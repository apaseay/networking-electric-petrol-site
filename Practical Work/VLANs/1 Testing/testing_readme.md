## Testing

### What is the default native VLAN?

On Cisco switches, the **default native VLAN is VLAN 1**.  
Although the command `switchport trunk native vlan 999` changes the native VLAN in use on a trunk, it does **not change the Cisco default**, which remains VLAN 1 unless explicitly reconfigured.

---

### Why don’t we use VLAN 1?

VLAN 1 is avoided because it is associated with **default control-plane and proprietary protocols** on Cisco switches.  
According to Proprietary Protocol Attacks notes, several Cisco protocols such as **VTP, DTP, PVLAN, and CDP** have well-known attack vectors.

Using VLAN 1 for management or as the native VLAN increases **security risk** and the likelihood of **misconfiguration**.  
Best practice is to move management traffic to a dedicated VLAN and use an unused VLAN (e.g. VLAN 999) as the native VLAN.