## Port Security – Evading Security (Command Explanation)

interface FastEthernet0/5
# Selects the physical switch port being configured.

description XXXXXXXXX
# Adds an administrative label describing what is connected to the port.

switchport access vlan 5
# Assigns the port to VLAN 5.

switchport mode access
# Forces the port into access mode so it supports a single VLAN (not trunking).

switchport port-security
# Enables Port Security on the interface to restrict allowed MAC addresses.

switchport port-security aging time 2
# Sets the aging timer for secure MAC addresses to 2 minutes.

switchport port-security violation restrict
# Drops traffic from unauthorised MAC addresses while keeping the port up and logging the violation.

switchport port-security aging type inactivity
# Removes learned MAC addresses only if no traffic is seen during the aging period.

macro description cisco-desktop
# Applies a predefined Cisco interface macro for desktop access ports.