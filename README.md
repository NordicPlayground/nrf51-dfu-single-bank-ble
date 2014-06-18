nRF51-SingleBankDFU-BLE
=======================

Single bank bootloader for DFU over BLE (nRF51, S110 v6.x)

Based on the dual bank BLE bootloader example in SDKv5.2.0.

Modification added to use the dfu_single_bank.c 
Please look for the comments "SINGLEBANK PATCH" in the code

Main difference was that bank0 will be erased when the image file is received. Only the pages that covered by the image size is deleted.
The master would need to wait until the peripheral finishes deleting the pages and send a notification (image size response) before starting to send image data. 
This causes the DFU on the Master Control Panel PC app incompatible. Because it doesn't wait for the notification after sending image size.
Modification needed on the PC software to wait at least 15 second before sending image data, or wait for the notification as in the Android app or iOS app. 

Tested with Android nRFToolbox, nRFMaster Control Panel, iOS Loader, iOS nRFToolbox
