# Analysis of Scanned Network with details on protocol

## When your host boots, it uses the DHCP protocol to obtain networking configuration information including: 

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

**Start a capture in Wireshark**

Issue the following command in a terminal window: 

_sudo dhclient –r ens32 _

This command releases the IP address currently associated with interface ens32 on your virtual machine.     

Next, 
**issue a new DHCP request with the command: **
_sudo dhclient ens32 _

Stop the Wireshark capture and save the capture file.  Name this file “dhcp”.  

**Find the frames associated with the DHCP request.  You are looking for frames using the DHCP protocol issuing the Discover, Offer, Request, and Acknowledge (DORA).  If you want, you can filter the packets by entering bootp for the filtering criteria to help narrow down your search.  DHCP is basically an extended version of the old BOOTP protocol. **  

Select the DHCP Offer frame and expand the Bootstrap Protocol information in the Wireshark Packet Details window.   

Q1.1: What IP address was offered to your client?  (Look for “Your (client) IP address”.) 

10.2.56.199 

Q1.2: What Subnet Mask was offered to your client?  

255.255.248.0 

Q1.3: What is the IP address lease time? 

1 hour 

Q1.4: What DNS servers are included in the offer?  (List all of them.) 

172.28.102.11 

172.28.102.13 

10.11.0.51 

10.14.1.10 

Q1.5: What is the default gateway? (It’s labeled “Router” in the Packet Details Window.) 

10.2.56.1 

Q1.6: What is the domain name? 

hh.nku.edu 
