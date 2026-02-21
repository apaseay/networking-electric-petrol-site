# Port Security - Expalantion
## What the Commands Do

### First set of commands (gi1/0–3)
These ports are set for normal devices.  
Each port learns the first device connected to it and remembers its MAC address.  
If a different device is plugged in, its traffic is blocked, but the port remains active.

### Second set of commands (gi2/0–3)
These ports allow up to three devices per port.  
If more than three MAC addresses are detected, the port is automatically shut down for security.

### Overall Purpose
The commands are used to control which devices can connect to switch ports and to protect the network from unauthorized access.





## Post Security Verification - Switch23
The command `show port-security interface gi1/3` was used to check security status of the port.
The output shows that port security is configured but no device is currently connected, so no MAC address has been learned yet.
The violation mode is set to shutdown, meaning the port will disable itself if an unauthorized device is detected.

No security violations have occurred at this stage.