## Monitoring
	Increase TX Power
		iw reg set B0; iwconfig wlan0 txpower 30
	Monitor 2.4GHz (w/ channel hopping)
		airodump-ng mon0
	Monitor 5GHz (w/ channel hopping)
		airodump-ng --band a mon0
	Monitor specific Channel
		airodump-ng -c <channel> mon0
	Monitor Clients on AP
		airodump-ng -c <channel> --bssid <MAC_AP> -w <capture_file> mon0
	Find Hidden SSID
		airodump-ng –c <channel> --bssid <MAC_AP> mon0
		aireplay-ng -0 20 –a <MAC_AP> mon0 
	All-in-one w/ web UI
		kismet -c mon0
	Generate Graph of Probe Requests of nearby Devices
		airodump-ng -r targetnet.pcap -w TARGETNET
        airgraph-ng -i TARGETNET-01.csv -g CPG -o targetnet-pnl.png
		Interesting to rebuild devices' PNLs & spawn rogue AP in smart way
	Wardriving
		https://wigle.net
