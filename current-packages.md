# Current WLAN Pi Packages

As part of the migration to the WLAN Pi V2 code, I'm conducting an audit of existing packages that we use up to v1.9.1 so that we can document how they are currently installed and operated so that we can plan how they will need to be packaged and migrated to v2. It will also assist with planning how we stop/start various processes & packages, and how they will need to interact with the FPMS & Web GUI.  


## Existing Linux packages

- tcpdump: 
- tshark
- iperf2
- iperf3
- eperf
- zap
- aircrack-ng
- kismet
- Bettercap

## Project-hosted packages:

- profiler
- fpms
- wconsole
- wlanpihotspot
- pkg-admin-tools
- misc-build-files
- web-front-end
- speedtest


## 3rd party modules installed on WLAN Pi

- WFE 
- wiperf


## 3rd party modules not installed on WLAN Pi, but used with WLAN Pi

- extcap: plugin for Wireshark on Mac that allows WLAN Pi to be used as remote capture device (also good for Windows if Python installed on Windows machine)
    - Site: https://github.com/adriangranados/wlan-extcap
    - Dependencies (packages on WLAN Pi):
        - ssh
        - iw
        - tcpdump
- wlan-extcap-win: plugin for Wireshark on Windows that allows WLAN Pi to be used as remote capture device
    - Site: https://github.com/wifinigel/wlan-extcap-win
    - Dependencies (packages on WLAN Pi):
        - ssh
        - iw
        - tcpdump