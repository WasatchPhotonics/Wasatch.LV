# Overview

LabVIEW NXG support is developmental.  We were able to get Wasatch.NET 2.1.8 
working with LabVIEW NXG 4.0, but only by manually adding WasatchNET, 
LibUsbDotNet and MPSSELight to GAC.

# Notes

LabVIEW only supports .NET assemblies in the GAC.  The Wasatch.NET installer does 
not currently auto-install in the GAC; we may need to update from Visual Studio 
Installer projects to WiX for that.

I was able to manually install a strongly-named build of WasatchNET to the GAC by 
running:

    % which gacutil
    /c/Program Files (x86)/Microsoft SDKs/Windows/v10.0A/bin/NETFX 4.6.1 Tools/gacutil

    % gacutil /u WasatchNET.dll

That allowed NXG to load WasatchNET.dll from the GAC.  However, it then barfed as
two dependent DLLs (LibUsbDotNet and MPSSELight) were themselves not in the GAC...
and I couldn't add them, as they weren't strongly named either.

Solution: (repeat for MPSSELight)

    C:\Program Files\Wasatch Photonics\Wasatch.NET>ildasm LibUsbDotNet.dll /out:LibUsbDotNet.il
    C:\Program Files\Wasatch Photonics\Wasatch.NET>ren LibUsbDotNet.dll LibUsbDotNet.old
    C:\Program Files\Wasatch Photonics\Wasatch.NET>C:\Windows\Microsoft.NET\Framework\v4.0.30319\ilasm LibUsbDotNet.il /dll /key=WasatchPub.snk
    Microsoft (R) .NET Framework IL Assembler.  Version 4.7.3190.0
    Copyright (c) Microsoft Corporation.  All rights reserved.
    Assembling 'LibUsbDotNet.il'  to DLL --> 'LibUsbDotNet.dll'
    Writing PE file
    Signing file with strong name
    Operation completed successfully

(Note: the signed DLL dependencies need to then be used to build a new 
WasatchNET.dll, and all added to the GAC.  This allowed NXG to "see" WasatchNET
with no errors, although a number of "coerced wire type" warnings remain.)

# References

NXG documentation appears to be developmental, but these were helpful.

- https://ni.i.lithium.com/t5/image/serverpage/image-id/206152iD06D039E5CC7FDEB/image-size/original?v=1.0&px=-1
- http://www.geekzilla.co.uk/ViewCE64BEF3-51A6-4F1C-90C9-6A76B015C9FB.htm
