---
parent: Tasmota
---
## Basic Settings and Setoptions

After setting up 'fresh' Tasmota on a device, the following SetOptions (SO) and Settings may be considered;

Usage: SOXX 1 to activate and SOXX 0 to deactivate the desired SO. These should be entered in the tasmota console.

`SO65 1`
To disable Device recovery using fast power cycle detection. Use this if your device reverts to AP mode after a voltage fluctuation cycle. Alert: This takes away the ability for fast power cycle detection (Power the device on and off six times with intervals lower than 10 seconds and leave it on after seventh time) to reset the device.

`SO1 1`
To disable inadvertent device reset due to long press of a 'Button'.

`Timezone +05:30`
To set Tasmota time to IST.

`SO56 1`
Wi-Fi network scan to select strongest signal on device restart (network has to be visible).
