# AC current measurement using ACS712

ACS712 is one of the cheapest available current measurement sensor in the market. It operates by returning an analog value proportional to the current being passed with a fairly low response time of 5us. [Datasheet](https://www.sparkfun.com/datasheets/BreakoutBoards/0712.pdf)

Given the output from the sensor is also an analog output, it is tricky to do current calculations on top of this sensor. This is because the output would be similar to the AC waveform input. However, you can use the method below to get a fairly well calibrated system which is quite accurate. The details are based on this well explained [research](https://create.arduino.cc/projecthub/SurtrTech/measure-any-ac-current-with-acs712-70aa85), I will focus only on the final result of using it in your system and not the why, you can read more in the linked tutorial. We will use the final version listed as "Test 3" in the tutorial above so it works even with dimmer circuits that use Triacs. 
Note: This requires adding some additional libraries in your ESPHome config, this can lead to a limited RAM availability. I wasn't able to run BLE monitor when adding these libraries on my ESP32 board. 

### Step 1: Include required libraries
[Download the filters library](https://github.com/JonHub/Filters) and place it in `config/esphome/` folder.

### Step 2: Create custom header file with sensor
You can name it as `acs_trms.h` and again place it in `config/esphome/` folder

```
#include "Filters.h"

class MyTRMSSensor : public PollingComponent, public Sensor {
    float ACS_Value;                              //Here we keep the raw data valuess
    float testFrequency = 50;                    // test signal frequency (Hz)
    float windowLength = 120.0/testFrequency;     // how long to average the signal, for statistist

    float intercept = -70; // to be adjusted based on calibration testing
    float slope = 15.4; // to be adjusted based on calibration testing
      
    float Amps_TRMS; // estimated actual current in amps

    // Track time in milliseconds since last reading 
    unsigned long previousMillis = 0;

  public:
    RunningStatistics inputStats = RunningStatistics();
    MyTRMSSensor() : PollingComponent(6000) {}

    float get_setup_priority() const override { return esphome::setup_priority::HARDWARE; }
  
   float read_Amps() {                       
      return intercept + slope * inputStats.sigma();
   }

    void setup() override {
      inputStats.setWindowSecs( windowLength );     //Set the window length
    }
  
    void update() override {
      publish_state(read_Amps());
    }
  
    void loop() override {
      ACS_Value = analogRead(35);  // read the analog value from pin 35
      inputStats.input(ACS_Value);  // log to Stats function
    }
};
```

### Step 3: Create ESPHome device YAML file
```
esphome:
  name: power-strip
  platform: ESP32
  board: esp-wrover-kit
  includes:
    - Filters.h
    - FilterOnePole.h
    - FilterTwoPole.h
    - FilterDerivative.h
    - RunningStatistics.h
    - FloatDefine.h
    - FilterOnePole.cpp
    - FilterTwoPole.cpp
    - FilterDerivative.cpp
    - RunningStatistics.cpp
    - acs_trms.h
    
sensors:
  - platform: custom
    lambda: |-
      auto my_sensor_rms = new MyTRMSSensor();
      App.register_component(my_sensor_rms);
      return {my_sensor_rms};

    sensors:
      name: "Powerstrip current TRMS"
      unit_of_measurement: "mA"
      accuracy_decimals: 2

```

### Step 4: Tuning
Use a known load or an existing smart plug and tune your slope and intercept in `acs_trms.h`. First tune your intercept by having 0 load, and then tune your slope by adding some known load and checking the value you get.

