# Wireguard
WireGuard is a VPN protocol — the way that a client (like your computer or phone) communicates with a VPN server. Wireguard was merged into the Linux 5.6 kernel in March 2020.
Wireguard basically can be used to create tunnel between two namespace. WireGuard uses ChaCha20 for symmetric encryption with Poly1305 for message authentication.
Our task in this project is to connect two interfaces which are present in different network through wireguard VPN. 

## Step 1
Created 2 network namespaces on Ubuntu machine (red , blue). We connected those 2 namespaces using virtual ethernet allowing the connectivity between two namespaces. Assigned the ip addresses. Then we created 2 wireguard interfaces (wg0 , wg1) in each network namespace. We assigned the ip addresses to each wireguard interface. We generated different private keys for each namespace and assigned those keys to each namespace. We generated the public keys for each namespace. We configured the interfaces (wg0 , wg1) exchanging the public keys generated on each namespace. We specified the endpoint ip addresses and their port numbers (interfaces were running on same machine but on different port numbers) for each namespace. We pinged from red namespace to blue namespace on the address of wireguard interface. The ping was successful.       
