# Current WLAN Pi Packages

As part of the migration to the WLAN Pi V2 code, I'm conducting an audit of existing packages that we use up to v1.9.1 so that we can document how they are currently installed and operated so that we can plan how they will need to be packaged and migrated to v2. It will also assist with planning how we stop/start various processes & packages, and how they will need to interact and intergate with the FPMS & Web GUI.  

(Note that where Python module dependencies are specified, these are modules that are not part of the standard library)


## Linux (Armbian) Packages Added to Base Image

- **tcpdump**: 
    - Installation method: apt-get
    - Comments: Used for remote wireshark capture tools
- **isc-dhcp**: 
    - Installation method: apt-get
    - Comments: required for hostspot & wconsole
- **hostapd**:
    - Installation method: apt-get
    - Comments: required for hostspot & wconsole
- **tshark**:
    - Installation method: apt-get
- **aircrack-ng**:
    - Installation method: apt-get
- **Scapy**:
    - Function: Debian package installation of Scapy for CLI 
    - Installation method: apt-get
    - Comments: Retire (don't install) - will be installed as required by Python packages that need it using pip
- **Python3**:
    - Installation method: native to Armbian image
    - Comments: 3.7 will be native to new image, latest updates available will be pulled in using "apt-get update"
- **Python2**:
    - Installation method: native to Armbian image
    - Comments: Deprecated, will be removed from new WLAN Pi images
- **iperf3**:
    - Installation method: apt-get
    - Comments: Currently starts from cron startup - in future enable/disable from Cockpit
- **ser2net**
    - Installation method: apt-get
    - Comments: Provide network access to device serial ports

## Project-hosted packages:

- **profiler**: Python script that performs assessment of client capabilities based on analysis of client association frame (Note: this is due to be replaced by profiler2 which is in development: https://github.com/joshschmelzle/profiler2)
    - Repo: https://github.com/WLAN-Pi/profiler
    - Dependencies:
        - Python modules: scapy, manuf, fakeap, pymongo 
    - Control mechanisms: start/stop profiler script via FPMS. Needs to be controlled by systemctl in new image release 
- **fpms**: Python scripts/modules that provide the front panel menu system that is operated via the 3 buttons of the WLAN Pi. (Note this replaces the previous Bakebit repo that was used for the front panel menus https://github.com/WLAN-Pi/BakeBit). This new package has not been used for a WLAN Pi image as yet - image v1.9.1 used he previous Bakebit repo version
    - Repo: https://github.com/WLAN-Pi/fpms
    - Dependencies:
        - Python modules: PIL, bakebit_128_64_oled, types, re, textwrap, subprocess, signal, socket
- **Wi-Fi Console**: Turns your WLAN Pi in to a wireless serial console
    - Repo: https://github.com/WLAN-Pi/wconsole
    - Dependencies: isc-dhcp-server, ser2net, hostapd
    - Control mechanisms: Relies on global mode switch that maps various network files be changed (via symbolic links) and a reboot of the WLAN Pi unit for changes to take effect
- **wlanpihotspot**:
    - Repo: https://github.com/WLAN-Pi/wlanpihotspot
    - Dependencies: hostapd, isc-dhcp
    - Control mechanisms: Relies on global mode switch that maps various network files be changed (via symbolic links) and a reboot of the WLAN Pi unit for changes to take effect
    - Comments: Short term, migrate as-is to new image. Long term move to replace with RaspAP: RaspAP - https://github.com/billz/raspap-webgui
- **pkg-admin-tools**: 
    - Repo: https://github.com/WLAN-Pi/pkg-admin-tools
    - Dependencies: Python3
    - Comments : Do not move to new WLAN Pi image - replicate feaure with standardized Debian packaging
- **misc-build-files**: A collection of miscellaneous Linux config files that have been customised for the WLAN Pi. They were placed in this repo to ensure they did not get missed each time a new image build was completed. The files are installed using the pkg_admin tool.
    - Repo: https://github.com/WLAN-Pi/misc-build-files
    - Dependencies: None
    - Comments: Do not move to new WLAN Pi image - will be replaced by standard image build process (but make sure settings are included in new image build)
- **web-front-end**:
    - Repo: https://github.com/WLAN-Pi/web-front-end
    - Comments: Do not move to new WLAN Pi image - will be replaced by new web GUI
- **speedtest**: HTML5 Speedtest forked from https://github.com/librespeed/speedtest. Files are served by the WLAN Pi Apache web server - there are no server-side scripts or processes.
    - Repo: https://github.com/WLAN-Pi/speedtest
    - Dependencies: Apache web server
    - Comments: Need to incorporate in to new Web GUI. Long term: embellish to store data, look at history etc.
- **Bakebit**:
    - Repo: https://github.com/WLAN-Pi/BakeBit
    - Comments: Replaced by the fpms project which provides streamlined repo and Python 3 support


## 3rd party modules installed on WLAN Pi

- **wifiexplorer-sensor**: package that allows WLAN Pi to be used as a remote sensor for WifiExplorer
    - Site: https://github.com/adriangranados/wifiexplorer-sensor
    - Dependencies: Python3, python3-pip
    - Comments: Migrate to new image as-is, ideally packaged up as Debian package
- **wiperf**: 
    - Function: package that allows the WLAN Pi to gather UX data for both wireless & ethernet network connections
    - Site: https://github.com/wifinigel/wiperf
    - Dependencies: Python3
    - Control mechanisms: Relies on global mode switch that maps various network files be changed (via symbolic links) and a reboot of the WLAN Pi unit for changes to take effect
    - Comments: Migrate to new image as-is, ideally packaged up as Debian package
- **kismet**:
    - Function: WLAN audit/security
    - Installation method: Compiled from source
    - Comments: Retire from future images - provide instructions of how to install for those that need/want 
- **Bettercap**:
    - Function: Security toolset
    - Installation method: Compiled from source (uses Go)
    - Comments: Retire from future images - provide instructions of how to install for those that need/want 
- **H.O.R.S.T**: 
    - Function: lightweight 802.11 wireless LAN analyzer with a text interface
    - Installation method: Compiled from source
    - Comments: Retire, only supports up to 11n so has limited usefulness
- **Termshark**: 
    - Function: terminal UI that provides Wireshark-type experience https://termshark.io/
    - Installation method: Compiled from source (uses Go)
    - Comments: Retire from standard WLAN Pi image - resource intensive, limited usefulness
- **iperf2**:
    - Source page: https://sourceforge.net/p/iperf2/code/ci/master/tree/
    - Installation method: custom build/compile for WLAN Pi image to get latest version
    - Comments: Currently starts from cron startup - in future enable/disable from Cockpit
- **eperf**:
    - Home page: https://sw.ekahau.com/download/eperf/ (uses Java, requires JRE)
    - Installation method: unzip
    - Comments: Candidate for removal from future releases - eats lots of resource as requires JRE installation - Jerry to test to see if iperf3 is good enough so that eperf could be removed
- **Ruckus Speedflex(Zap)**:
    - Installation method: Compiled from source
    - Comments: Retire from future images - provide instructions of how to install for those that need/want it 

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