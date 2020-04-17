# Current WLAN Pi Packages

As part of the migration to the WLAN Pi V2 code, I'm conducting an audit of existing packages that we use up to v1.9.1 so that we can document how they are currently installed and operated so that we can plan how they will need to be packaged and migrated to v2. It will also assist with planning how we stop/start various processes & packages, and how they will need to interact and intergate with the FPMS & Web GUI.  

(Note that where Python module dependencies are specified, these are modules that are not part of the standard library)


## Linux Packages Added to Base Image

- tcpdump: 
- tshark
- iperf2
- iperf3
- eperf
- zap
- aircrack-ng
- kismet
- Bettercap
- Scapy
- Python3

## Project-hosted packages:

- **profiler**: Python script that performs assessment of client capabilities based on analysis of client association frame (Note: this is due to be replaced by profiler2 which is in development: https://github.com/joshschmelzle/profiler2)
    - Repo: https://github.com/WLAN-Pi/profiler
    - Dependencies:
        - Python modules: scapy, manuf, fakeap, pymongo 
- **fpms**: Python scripts/modules that provide the front panel menu system that is operated via the 3 buttons of the WLAN Pi. (Note this replaces the previous Bakebit repo that was used for the front panel menus https://github.com/WLAN-Pi/BakeBit). This new package has not been used for a WLAN Pi image as yet - image v1.9.1 used he previous Bakebit repo version
    - Repo: https://github.com/WLAN-Pi/fpms
    - Dependencies:
        - Python modules: PIL, bakebit_128_64_oled, types, re, textwrap, subprocess, signal, socket
- **Wi-File Console**: https://github.com/WLAN-Pi/wconsole
    - Repo: https://github.com/WLAN-Pi/wconsole
    - Dependencies: isc-dhcp-server, ser2net, hostapd
- **wlanpihotspot**:
- **pkg-admin-tools**:
- **misc-build-files**:
- **web-front-end**:
- **speedtest**:


## 3rd party modules installed on WLAN Pi

- **wifiexplorer-sensor**: package that allows WLAN Pi to be used as a remote sensor for WifiExplorer
    - Site: https://github.com/adriangranados/wifiexplorer-sensor
    - Dependencies: Python3, Scapy
- **wiperf**: package that allows the WLAN Pi to gather UX data for both wireless & ethernet network connections
    - Site: https://github.com/wifinigel/wiperf
    - Dependencies: 


## 3rd party modules not installed on WLAN Pi, but used with WLAN Pi

- **wlan-extcap**: plugin for Wireshark on Mac that allows WLAN Pi to be used as remote capture device (also good for Windows if Python installed on Windows machine)
    - Site: https://github.com/adriangranados/wlan-extcap
    - Dependencies (packages on WLAN Pi):
        - ssh
        - iw
        - tcpdump
- **wlan-extcap-win**: plugin for Wireshark on Windows that allows WLAN Pi to be used as remote capture device
    - Site: https://github.com/wifinigel/wlan-extcap-win
    - Dependencies (packages on WLAN Pi):
        - ssh
        - iw
        - tcpdump