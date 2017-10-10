![Diagram View](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/diagram.png)

# Overview

LabVIEW demos and solutions using Wasatch Photonics spectrometers.

# Dependencies

The LabVIEW demo requires [Wasatch.NET](https://github.com/WasatchPhotonics/Wasatch.NET/).

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

* C:\\Program Files\\Wasatch Photonics\\Wasatch.NET\\WasatchNET.dll
* C:\\Program Files (x86)\\Wasatch Photonics\\Wasatch.NET\\WasatchNET.dll

![Panel View](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/panel.png)
