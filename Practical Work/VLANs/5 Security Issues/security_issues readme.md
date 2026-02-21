## Security Issues

VLAN Creation Attempt (VTP Behaviour)

An attempt was made to create VLANs on all three switches to determine where VLAN database changes were permitted.
	•	Switch21 → VLAN creation denied (VTP client mode)
	•	Switch22 → VLAN creation denied (VTP client mode)
	•	Switch23 → VLAN creation denied (not permitted to modify the VLAN database)



 VLAN creation is currently blocked by VTP configuration. 
 No switch is permitting VLAN database changes

### Discard VLAN and Port Shutdown

An attempt was made to create a Discard VLAN (VLAN 1000) on Switch23. VLAN creation was restricted by VTP configuration. This removes unused ports from VLAN 1 and reduces the risk of unauthorized access.

Unused access ports (gi0/0, gi0/2, gi0/3) were assigned to the discard policy and administratively shut down. Testing confirmed that ports gi0/2 were disabled and could not be used for connectivity.



