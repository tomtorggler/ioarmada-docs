# VMware Drivers

# WDS

Add boot image from 2016TP5 iso.

Add pvscsi and vmxnet3 to the boot image using dism.exe from the iso.

```
mkdir C:\Mount 
.\dism /Mount-Wim /WimFile:"C:\RemoteInstall\Boot\x64\Images\boot.wim" /Index:1 /MountDir:C:\Mount 
.\dism /Image:C:\Mount /Add-Driver /Driver:"C:\vmware\vmxnet3ndis6.inf" 
.\dism /Image:C:\Mount /Add-Driver /Driver:"C:\vmware\pvscsi.inf" 
.\dism /Unmount-Wim /Commit /MountDir:C:\Mount
```

Then again for \/Index:2

