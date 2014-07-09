nRF51-SingleBankDFU-BLE
=======================

Single bank bootloader for DFU over BLE (nRF51, S110 v6.x)

Based on the dual bank BLE bootloader example in SDKv5.2.0.

Modification added to use the dfu_single_bank.c 
Please look for the comments "SINGLEBANK PATCH" in the code

Main difference was that bank0 will be erased when the image size is received. Only the pages that covered by the image size is deleted.
The master would need to wait until the peripheral finishes deleting the pages and send a notification (image size response) before starting to send image data. 
This causes the DFU on the Master Control Panel PC app incompatible. Because it doesn't wait for the notification after sending image size.
Modification needed on the PC software to wait at least 10 seconds before sending image data, or wait for the notification as in the Android app or iOS app. 

Tested with Android nRFToolbox, nRFMaster Control Panel, iOS Loader, iOS nRFToolbox

Requirements
------------
- nRF51 SDK version 5.2.0
- nRF51822 Development Kit version 2.1.0 or later

The project may need modifications to work with other versions or other boards. 

To compile it, clone the repository in the \nrf51822\Board\nrf6310\device_firmware_updates folder.

About this project
------------------
This application is one of several applications that has been built by the support team at Nordic Semiconductor, as a demo of some particular feature or use case. It has not necessarily been thoroughly tested, so there might be unknown issues. It is hence provided as-is, without any warranty. 

However, in the hope that it still may be useful also for others than the ones we initially wrote it for, we've chosen to distribute it here on GitHub. 

The application is built to be used with the official nRF51 SDK, that can be downloaded from https://www.nordicsemi.no, provided you have a product key for one of our kits.

Please post any questions about this project on https://devzone.nordicsemi.com.
