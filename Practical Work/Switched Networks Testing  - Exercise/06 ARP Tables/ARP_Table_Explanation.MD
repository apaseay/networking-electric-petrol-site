# ARP Tables – PC1

## When ARP did not return any output
At the start of the testing, running the `arp` command on PC1 returned no output.  
This indicated that the ARP table was empty because no communication had yet taken place.

After pinging the other devices on the network, including PC2 and the managed switches, the ARP table became populated.  
Each entry showed an IP address mapped to a MAC address, along with a timer showing how long the entry would remain valid.

**Evidence:**  
/Users/apase/ATU PROJECTS/Networking/Switched Networks Testing : Exercise/06 ARP Tables/PC1_ARP_Table_After_Pings.png

## Explanation
Initially, the ARP table was empty because PC1 had not communicated with any other devices on the network.

When PC1 pinged each device, it needed to find the MAC address associated with each IP address.  
ARP was used to discover this information, and the results were stored in the ARP table.

Once these entries were created, PC1 could communicate with the devices without needing to repeat the ARP process immediately.

The timers shown in the ARP table indicate that entries are temporary and will be removed automatically after a period of inactivity.

## What I Observed
The ARP table is built dynamically as devices communicate on the network and remains empty until traffic is generated.








# ARP Table – Switch21

## Explanation
After pinging all devices on the network from Switch21, the ARP table became populated with entries for each device.

Each entry shows the IP address of a device and the MAC address it is associated with.  
These entries appeared only after the ping commands were run.

This shows that Switch21 learned the MAC addresses dynamically by communicating with each device.  
The age values indicate that the entries are temporary and will be removed if the devices are not contacted again.

**Evidence (Screenshot):**  
/Users/apase/ATU PROJECTS/Networking/Switched Networks Testing : Exercise/06 ARP Tables/Switch21_ARP_Table_After_Pings.png