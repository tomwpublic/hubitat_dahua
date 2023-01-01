# hubitat_dahua

This package provides a Hubitat integration for Dahua-supplied IP cameras, including Dahua and Amcrest cameras and doorbells.  It may work with other brands that are Dahua cameras under the hood.

Supported capabilities include ImageCapture, MotionSensor, PushableButton (for doorbells), cross line detection, cross region detection, and object detection (if supported by your camera).

All events are based on real-time events pushed from the camera.  There is no polling for events or status.

Thanks to techbill from the Hubitat forums for all of their testing, feedback, and suggestions.  And thanks to mluck for the inspiration.

# Manual Installation instructions:

Installing with Hubitat Package Manager (HPM) is recommended. 

If you must install manually, follow these steps:

* In the *Drivers Code* section of Hubitat, install the *cameraDriver*.    
* (Optional) If you want to use auto-discovery features with multiple cameras, install the *cameraDiscoveryApp* in the *Apps Code* section of Hubitat.  Skip to the section below on using the camera discovery app.

# Virtual Device configuration instructions:

* In the *Devices* section of Hubitat, add a *New Virtual Device* of type Dahua/Amcrest Camera.
* On the virtual device page, set the preferences:
    * Enter the IP and port number of your camera.
    * Enter the login credentials of your camera.  This should be the same username and password that you use to log in to the web interface of the camera by entering its IP.
    * Save Preferences and then refresh the page.  The name of the virtual device should be updated to match the name of your camera.
* Note that some recent firmware versions have removed or disabled local API access.  So, if your camera does not respond correctly, try another firmware version and/or camera.

# Usage instructions (virtual device):

* Use the `take` command to take a snapshot from the device.
* Observe events on the `motion` attribute (for video motion) and `smartDetectType` attribute (for AI object detection).
* Observe events on the attribute `crossLineDetected`and `crossRegionDetected` attributes, which will report the names of those events.
* For doorbell devices, the first physical button press on the doorbell will create a child virtual button controller.
    * Observe `pushed` events on button 1 for doorbell button press events.
* The `closeStream` command will close the event stream from the device.
    * You can use this if you want to pause receiving real-time events for some reason.
    * `Initialize` will re-start the event stream.

# (Optional) Use the camera discovery app:

**Install the app**
* In the *Apps* section of Hubitat, click *Add User App* to actually install the *Dahua camera discovery* app.
* Enter the IP address, port, username, and password of your NVR or of a camera in your system.
* On the next page, you should see a list of all discovered cameras with an option to automatically create a virtual device for each.
    * The discovery process may intermittently miss certain cameras on your system.  Refresh the page to re-scan if necessary.
    * You will still need to visit each virtual device page to configure the specific camera settings.  Review the section above for virtual device configuration instructions.

# Disclaimer

I have no affiliation with any of the companies mentioned in this readme or in the code.
