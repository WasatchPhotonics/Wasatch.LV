![Diagram View](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/diagram.png)

# Overview

LabVIEW demos and solutions using Wasatch Photonics spectrometers.

# Dependencies

The LabVIEW demo requires [Wasatch.NET](https://github.com/WasatchPhotonics/Wasatch.NET/) 
(at writing, version 1.0.14 or later).

Please download and run either the 32-bit or 64-bit (see below) installer for Wasatch.NET
and follow the driver installation process before attempting to run the WastachDemo.vi.

# Architecture (Bitness)

This demo has been tested on LabVIEW 2017 32-bit under Windows 10 64-bit.  

If you are using 32-bit LabVIEW (the typical case, even on 64-bit Windows),
then you should install the 32-bit version of Wasatch.NET.

If you are using 64-bit LabVIEW, then you should install the 64-bit version of Wasatch.NET.

When you first open the WasatchDemo.vi, it may ask you to point it to the location of
WasatchNET.dll on your system.  That will typically be one of the following two paths,
depending on which version of the driver you installed:

- C:\\Program Files\\Wasatch Photonics\\Wasatch.NET\\WasatchNET.dll
- C:\\Program Files (x86)\\Wasatch Photonics\\Wasatch.NET\\WasatchNET.dll

# Common Errors

## No spectrometers found

Make sure that after installing Wasatch.NET, you 
[updated the device drivers](https://github.com/WasatchPhotonics/Wasatch.NET#post-install-step-1-libusb-drivers)
for your spectrometers.

## Error 1386 occured at Invoke Node: The specified .NET class is not available

Most common reason for this seems to be trying to use a 64-bit version of 
Wasatch.NET with a 32-bit version of LabVIEW, or vice-versa.

# Version History

- 2018-03-13 Tested against LabVIEW 2017 64-bit
- 2018-02-16 Added "Fire Laser" toggle; changed temperature from DBL to SGL
- 2017-12-05 Added check for no spectrometers (tested w/1.0.13)
- 2017-11-09 Updated setCCDTemperatureSetpointDegC (tested w/1.0.11)
- 2017-10-24 Added TEC control with limits (tested w/Wasatch.NET 1.0.8)
- 2017-10-11 Added detector temperature readout

![Panel View](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/panel.png)
