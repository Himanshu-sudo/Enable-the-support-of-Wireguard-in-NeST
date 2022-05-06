# Wireguard
WireGuard is a VPN protocol — the way that a client (like your computer or phone) communicates with a VPN server. Wireguard was merged into the Linux 5.6 kernel in March 2020.
Wireguard basically can be used to create tunnel between two namespace. WireGuard uses ChaCha20 for symmetric encryption with Poly1305 for message authentication.
Our task in this project is to connect two interfaces which are present in different network through wireguard VPN. 

## Simple Network Interfaces
WireGuard works by adding a network interface (or multiple), like eth0 or wlan0, called wg0 (or wg1, wg2, wg3, etc). This network interface can then be configured normally using ifconfig(8) or ip-address(8), with routes for it added and removed using route(8) or ip-route(8), and so on with all the ordinary networking utilities. The specific WireGuard aspects of the interface are configured using the wg(8) tool. This interface acts as a tunnel interface.

WireGuard associates tunnel IP addresses with public keys and remote endpoints. When the interface sends a packet to a peer, it does the following:

This packet is meant for 192.168.30.8. Which peer is that? Let me look... Okay, it's for peer ABCDEFGH. (Or if it's not for any configured peer, drop the packet.)
Encrypt entire IP packet using peer ABCDEFGH's public key.
What is the remote endpoint of peer ABCDEFGH? Let me look... Okay, the endpoint is UDP port 53133 on host 216.58.211.110.
Send encrypted bytes from step 2 over the Internet to 216.58.211.110:53133 using UDP.
When the interface receives a packet, this happens:

I just got a packet from UDP port 7361 on host 98.139.183.24. Let's decrypt it!
It decrypted and authenticated properly for peer LMNOPQRS. Okay, let's remember that peer LMNOPQRS's most recent Internet endpoint is 98.139.183.24:7361 using UDP.
Once decrypted, the plain-text packet is from 192.168.43.89. Is peer LMNOPQRS allowed to be sending us packets as 192.168.43.89?
If so, accept the packet on the interface. If not, drop it.
Behind the scenes there is much happening to provide proper privacy, authenticity, and perfect forward secrecy, using state-of-the-art cryptography.

## Step 1
Created 2 network namespaces on Ubuntu machine (red , blue). We connected those 2 namespaces using virtual ethernet allowing the connectivity between two namespaces. Assigned the ip addresses. Then we created 2 wireguard interfaces (wg0 , wg1) in each network namespace. We assigned the ip addresses to each wireguard interface. We generated different private keys for each namespace and assigned those keys to each wireguard interface (wg0 , wg1). We generated the public keys for each namespace. We configured the interfaces (wg0 , wg1) exchanging the public keys generated on each namespace. We specified the endpoint ip addresses and their port numbers (interfaces were running on same machine but on different port numbers) for each namespace. We pinged from red namespace to blue namespace on the address of wireguard interface. The ping was successful.       
