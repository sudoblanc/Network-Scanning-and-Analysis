# When your host boots, it uses the DHCP protocol to obtain networking configuration information including: 

1. IP Address 
2. Subnet Mask 
3. Default Gateway 
4. DNS Servers 
5. Domain Name 

When the networking services are initialized during the boot process, your host broadcasts a DHCP Discover.  This sends a broadcast to everything in your LAN that requests any listening DHCP servers to offer a set of configuration parameters.   Any listening DHCP servers will reply to your host with a DHCP Offer.  This offers a set of network configuration parameters for your host.  Your host replies with a DHCP Request that lets the DHCP server know that your host would like the offered network configuration parameters.  (Interestingly, this request is broadcast because if multiple DHCP servers send an offer, they will all get to find out which one your host selected.)  Finally, the DHCP server sends a DHCP Acknowledge that lets your host know that its request has been confirmed.   You can remember the sequence of events with the mnemonic DORA (Discover, Offer, Request, Acknowledge). To recap the sequence: 

- The client broadcasts a DHCP Discover 
- The DHCP server sends a DHCP Offer to the client 
- The client broadcasts a DHCP Request 
- The DHCP server sends a DHCP Acknowledge to the client 

In this part of the lab, you are going to use the dhclient command to release your current network parameters and then use dhclient again to request a new set using the DORA sequence.  We’ll use Wireshark to see the details of this interaction. 

