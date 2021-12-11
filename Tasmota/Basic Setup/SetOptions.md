---
parent: Tasmota
title: Basic Setups and SetOptions
---
## Basic Setups and Setoptions

After setting up 'fresh' Tasmota on a device, the following SetOptions (SO) may be considered;

Usage: SOXX 1 to activate and SOXX 0 to deactivate the desired SO. These should be entered in the tasmota console.

SO65 1 : To disable Device recovery using fast power cycle detection. Use this if your device reverts to AP mode after a voltage fluctuation cycle. Alert: This takes away the ability to toggle power 7 times to reset the device.

