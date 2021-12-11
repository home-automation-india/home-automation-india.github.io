After setting up Tasmota on a fresh device, the following SetOptions (SO) may be considered;
Usage: SO<XX> 1 to activate and SO<XX> 0 to deactivate

1. SO65 1 : To disable Device recovery using fast power cycle detection
            Use this if your device reverts to AP mode after a voltage fluctuation cycle
            Alert: This takes away the ability to toggle power 7 times to reset the device

