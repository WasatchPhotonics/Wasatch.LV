![Diagram View](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/NXG-diagram-editor.png)

# Overview

LabVIEW NXG support is developmental.  We were able to get Wasatch.NET 2.1.8 
working with LabVIEW NXG 4.0, but only by manually adding WasatchNET, 
LibUsbDotNet and MPSSELight to GAC.

# Notes

LabVIEW only supports .NET assemblies in the GAC.  The Wasatch.NET installer does 
not currently auto-register Wasatch assemblies in the GAC; we may need to update 
from Visual Studio Installer projects to WiX for that.

For now, I was able to manually install a strongly-named build of WasatchNET to the GAC by 
running:

    % which gacutil
    /c/Program Files (x86)/Microsoft SDKs/Windows/v10.0A/bin/NETFX 4.6.1 Tools/gacutil

    % gacutil /u WasatchNET.dll
    % gacutil /u MPSSELight.dll
    % gacutil /u LibUsbDotNet.dll

That allowed NXG to load WasatchNET.dll from the GAC.  

For additional information on Wasatch.NET driver signing, see Wasatch.NET docs.

# References

NXG documentation appears to be developmental, but these were helpful.

- https://ni.i.lithium.com/t5/image/serverpage/image-id/206152iD06D039E5CC7FDEB/image-size/original?v=1.0&px=-1

![Panel View](https://github.com/WasatchPhotonics/Wasatch.LV/raw/master/screenshots/NXG-panel.png)
