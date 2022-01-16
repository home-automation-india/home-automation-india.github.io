## Creating Automations for multi click actions

There are instances where the external inputs like buttons often have single or double actions, and more is needed. This can be achieved via some smart automations

automations.yaml
```
- alias: "zb_button_actions"
  id: zb_button_actions
  mode: restart
  trigger:
  - platform: state
    entity_id: sensor.zb_button_action
    to: 
    - single 
    - double
  condition: []
  action:
  - repeat:
      count: "{{ 1 if trigger.to_state.state == 'single' else 2 if trigger.to_state.state == 'double' }}"
      sequence:
      - service: counter.increment
        target:
          entity_id: counter.click_counter        
  - delay:
    # supports seconds, milliseconds, minutes, hours
      milliseconds: 1000
  - service: persistent_notification.create
    data:
      message: test {{ trigger.to_state.state }}
  - service: counter.reset
    target:
      entity_id: counter.click_counter  

- alias: "double_click_action"
  id: double_click_action
  mode: single
  trigger:
  - platform: state
    entity_id: counter.click_counter
    to: "2"
    for:
      seconds: 1
  condition: []
  action:
  - service: input_number.set_value
    target:
      entity_id: input_number.double_click_display
    data:
      value: 2
  - delay:
      seconds: 2
  - service: input_number.set_value
    target:
      entity_id: input_number.double_click_display
    data:
      value: 0

- alias: "triple_click_action"
  id: triple_click_action
  mode: single
  trigger:
  - platform: state
    entity_id: counter.click_counter
    to: "3"
    for:
      seconds: 1
  condition: []
  action:
  - service: input_number.set_value
    target:
      entity_id: input_number.triple_click_display
    data:
      value: 3
  - delay:
      seconds: 2
  - service: input_number.set_value
    target:
      entity_id: input_number.triple_click_display
    data:
      value: 0
```
 
Summary:
1. zb_button_actions  is the primary automation which captures any button event, for example 'single'  (can be anything) and starts of a counter. This counter is incremented until certain duration  - delay of 1000 ms here.  After this delay, the counter is reset, ready for next cycle of input 
2.  The "double_click_action" watches the state of the click counter for the count value of 2 which should not change until certain duration - 1 second here and triggers respective actions.  Note:  You might want to play around with the delay duration mentioned in "zb_button_actions" and match against it. 
3. Similarly for "triple_click_action", the state of the counter is observed for count value of 3. The delay for: seconds: 1 plays a critical part - when a counter is incrementing in zb_button_actions, it might invoke "double_click_action"  event when it reaches count value of 2.  Hence the need for min duration for delay defined in zb_button_actions (and kind of match the delay in  zb_button_actions) .  However, if the duration of delay put is relatively higher - say 1.5 /2 seconds in this example, this will not trigger the triple_click_action, as the click_counter will be reset to 0 after 1 second.
You can define more "click_actions" based on delay duration to wait for all the clicks in zb_button_actions. It will also be based on how your setup performance is and your comfortability in getting the number of clicks within that delay duraton. In my testing, three clicks are easily possible using Sonoff Button by invoking single press three times within 1 sec / 1000 ms.  Please do tinker around to get your comfortability 
4. The following actions in  "double_click_action" and "triple_click_action" are not needed, they are just so that in the UI, the input number slider value could be reset after they are triggered for better visual feedback
```
  - delay:
      seconds: 2
  - service: input_number.set_value
    target:
      entity_id: input_number.double_click_display
    data:
      value: 0
```
