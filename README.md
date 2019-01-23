![Diagram View](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/diagram.png)

# Overview

LabVIEW demos and solutions using Wasatch Photonics spectrometers.

# Dependencies

The LabVIEW demo requires [Wasatch.NET](https://github.com/WasatchPhotonics/Wasatch.NET/) 
(at writing, version 2.0.9 or later).

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

# Tutorial

Here's a quick tutorial on how to create a LabVIEW Virtual Instrument (.vi)
controlling Wasatch Photonics spectrometers using our Wasatch.NET DLL.

## Step 1: Create a blank .vi

![create](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-01-create.png)
![blank](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-02-blank.png)

## Step 2: From Block Diagram, Display the Functions Palette

![functions](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-03-functions.png)

## Step 3: Select Connectivity -> .NET -> Invoke Node from Functions Palette

![.NET](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-04-NET.png)
![invoke](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-05-invoke.png)

## Step 4: Drop the ".NET Invoke Node" control onto the Block Diagram

![drop](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-06-drop.png)

## Step 5: Browse to the .NET DLL for this Node

Now you have to tell LabVIEW which DLL will provide the functionality for this .NET node,
since it has no "incoming reference" from a previous node to infer such things.  Fortunately
you only have to do this once per .vi, and can share the reference thereafter.

![browse](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-07-browse.png)

## Step 6: Navigate to WasatchNET.dll

![navigate](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-08-dll.png)

## Step 7: Select the WasatchNET.Driver class

Here you select the top-level class exposed by WasatchNET.dll that you wish to reference
through the .NET Node.  The Driver class is what we want: it's the starting point from which
you can dig down into all the Wasatch.NET goodness.

These are the API docs for the WasatchNET.Driver class which we'll be using:

- [WasatchNET.Driver](http://www.wasatchphotonics.com/api/Wasatch.NET/class_wasatch_n_e_t_1_1_driver.html)

![driver](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-09-driver.png)

## Step 8: Select Driver.getInstance() Static Method

To actually call the Driver class's getInstance() static method, you can select it from the
"Method" drop-down.  Note that static methods are indicated with a leading [S].

![getInstance](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-10-getInstance.png)

## Step 9: Add some more .NET Invoke Node controls

Let's go ahead and drop several more .NET Invoke Node controls onto the block diagram.
We'll wire them up shortly to step through the spectrometer initialization sequence.

![invoke 3](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-11-invoke3.png)

## Step 10: Wire Driver Reference to Invoke Node

Wire the output reference from Driver.getInstance() to the input reference of the next
.NET Invoke Node control.  This will change the previously unlabeled .NET node into a
Driver node.  (It will infer its .NET class from the output type of Driver.getInstance).

![reference](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-12-reference.png)

## Step 11: Call Driver.openAllSpectrometers()

Select the openAllSpectrometers() method of your new Driver object.

![openAllSpectrometers](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-13-openAllSpectrometers.png)

## Step 12: Relay the Driver reference

Wire the "output" reference from the openAllSpectrometers() control into the input reference
on the next unlabeled Invoke Node control.  Note that we're not taking the _output_ of the
openAllSpectrometers() method (which is actually an integer count of spectrometers found),
but simply re-using and "passing along" the reference to our Driver singleton.

![reference](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-14-reference.png)

## Step 13: Call Driver.getSpectrometer()

Now that the control knows (from its reference) that it's a Driver object, select its 
getSpectrometer() method.

![getSpectrometer](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-15-getSpectrometer.png)

## Step 14: Create input parameter

Unlike previous methods we've called, the Driver.getSpectrometer() method takes an argument:
the integral index of the spectrometer we wish to control.  As long as you have at least one
Wasatch spectrometer connected to the computer, the first should be number 0, so we'll create
an integer constant "0" to pass into the getSpectrometer() method.

![create](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-16-create.png)
![zero](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-17-zero.png)

## Step 15: Create .NET Node Property

Just for variety, after calling all those .NET Invoke Node controls where we were calling
methods on our Wasatch.NET Driver object, let's go ahead and create a Property Node as well.
We'll then wire it up with a reference just like the others, and then select a property to
view (in this case, the spectrometer's serial number).

![property](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-18-property.png)
![references](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-19-references.png)
![serialNumber](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/LV-20-serialNumber.png)

Hopefully this is enough to get you started.  Feel free to browse the Wasatch.NET API
documentation here, since the .NET classes, methods and properties are identical whether
drawing LabVIEW .vi block diagrams or writing code in C#, MATLAB or other .NET languages.

- http://www.wasatchphotonics.com/api/Wasatch.NET/annotated.html

# Common Errors

## "an error occurred trying to load the assembly"

Note that LabVIEW requires all DLL dependencies to be together in the same folder.
Therefore, you should probably point to the WasatchNET.dll installed in 
C:\Program Files (x86)\Wasatch Photonics\Wasatch.NET, which has all dependent DLLs
grouped for convenience.

## No spectrometers found

Make sure that after installing Wasatch.NET, you 
[updated the device drivers](https://github.com/WasatchPhotonics/Wasatch.NET#post-install-step-1-libusb-drivers)
for your spectrometers.

## Error 1386 occured at Invoke Node: The specified .NET class is not available

Most common reason for this seems to be trying to use a 64-bit version of 
Wasatch.NET with a 32-bit version of LabVIEW, or vice-versa.

# Version History

- 2019-01-22 2.0.0
    - updated to support events and recovery from missing final trigger
    - tested against Wasatch.NET 2.0.9 (32-bit) on SiG and OEM-ARM
- 2018-09-25 
    - updated with external triggering (tested with Wasatch.NET 2.0.0 32-bit)
- 2018-03-14 
    - .vi tutorial to celebrate Pi Day
- 2018-03-13 
    - Tested against LabVIEW 2017 64-bit
- 2018-02-16 
    - Added "Fire Laser" toggle; changed temperature from DBL to SGL
- 2017-12-05 
    - Added check for no spectrometers (tested w/1.0.13)
- 2017-11-09 
    - Updated setCCDTemperatureSetpointDegC (tested w/1.0.11)
- 2017-10-24 
    - Added TEC control with limits (tested w/Wasatch.NET 1.0.8)
- 2017-10-11 
    - Added detector temperature readout

![Panel View](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/panel.png)
