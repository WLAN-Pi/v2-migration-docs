# V2 Migration Docs

**Documentation to assist with the transition from v1.9.1 to v2.0 of the WLAN Pi image.**

The move from the version 1.x image train to v2.0 will be used as an opportunity to improve and streamline the methods used to create the WLAN Pi image. It will also use standardized packaging methods to allow for ease of update of the image and its packages.

The new image will also move towards being more hardware agnostic, with the goal that the image can easily be applied to a number of Armbian platforms. This has become an important consideration as the NEO2 platform from FriendlyArm is no longer available, so a suitable successor is currently under investigation.

The move to v2.x will also be used as an opportunity to rationalize the packages that are provided as part of the out-of-the-box image. Several packages are either out of date or are generally unused, so will be removed to ease the support effort required for the WLAN Pi image. 

Docs:

- [Current package summary](current-packages.md)
- [Proposed new packages](proposed-new-packages.md)
- [Migration Summary Sheet (Google doc)](https://docs.google.com/spreadsheets/d/1ltta3WHbiVDCdsPBEXGHW24cyKPPLhiuhOZ9bs2jNHg/edit?usp=sharing)

