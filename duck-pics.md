# duck-pics

This challenge gave me a 'capture.pcapng' file
>got a capture on the chall author while engaging in "personal matters". see what you can find.

I opened the pcapng file in wireshark to see what I could notice

![Wireshark Screenshot](/duck-pic.png)

The first thing I noticed was that the protocal for every packet was USB.  
Based on the challenge description and this, I guessed that the pcap was a keyboard capture  

I decided to search how to analyze a keyboard pcap file.  
The first result I found was [this](https://github.com/TeamRocketIst/ctf-usb-keyboard-parser)  

I followed the steps described:

```
$ tshark -r ./capture.pcapng -Y 'usb.capdata && usb.data_len == 8' -T fields -e usb.capdata > usbPcapData
```

```
$ python usbkeyboard.py usbPcapData
#TO DO fill in
```
