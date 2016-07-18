# Download Nano Server VHD File

Download the Nano Server VHD file from the [TechNet Eval Center](https://www.microsoft.com/en-us/evalcenter/en-us), it is listed as a download option for Windows Server 2016 TP5.

# VMware Drivers

VMware drivers for networking and the paravirtual SCSI controller have to be injected into the VHD file as well as into the boot.wim used by WDS.

## VHD File

The following commands can be used to inject drivers into the VHD file downloaded above.

> Note: Run the following commands from a machine running TP5 or use the dism.exe from the TP5 iso \(\sources folder\)

```
mkdir C:\Mount
.\dism /Mount-Image /Imagefile:"C:\nano-tp5.vhd" /Index:1 /MountDir:C:\Mount 
.\dism /Image:C:\Mount /Add-Driver /Driver:"C:\vmware\vmxnet3ndis6.inf" 
.\dism /Image:C:\Mount /Add-Driver /Driver:"C:\vmware\pvscsi.inf" 
.\dism /Unmount-Image /Commit /MountDir:C:\Mount
```

## Windows Deployment Services

The easies method to deploy Nano Server at this point is to use WDS, so to get the first Nano Server up and running, install the WDS and DHCP roles and add the boot image from the 2016TP5 iso. Use the following commands to inject VMware drivers into the boot image.

> Note: Run the following commands from a machine running TP5 or use the dism.exe from the TP5 iso \(\sources folder\)

```
mkdir C:\Mount 
.\dism /Mount-Wim /WimFile:"C:\RemoteInstall\Boot\x64\Images\boot.wim" /Index:1 /MountDir:C:\Mount 
.\dism /Image:C:\Mount /Add-Driver /Driver:"C:\vmware\vmxnet3ndis6.inf" 
.\dism /Image:C:\Mount /Add-Driver /Driver:"C:\vmware\pvscsi.inf" 
.\dism /Unmount-Wim /Commit /MountDir:C:\Mount
```

Note: Run the above commands again, specifying \/Index:2 when mounting the .wim file.

# Deploy

At this point, we are ready to deploy a new Nano Server virtual machine using WDS. So first, lets create a new virtual machine with the following specifications:

* 4 vCPU

* 4GB Memory

* 140GB Hard Disk

* VMware Paravirtual SCSI Controller

* vmxnet3 Network Adapter


Start the VM and connect to a console window. As no operating system should be present, the VM should PXE boot and the Nano Server image can be installed from WDS. Once installed, log into the Nano Server console using Administrator without password. The password must be reset upon first login:

![](/assets/nano_login_change_pw.png)

