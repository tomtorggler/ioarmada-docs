# Get IP Address

To get the IP address of the deployed worker node, log into the VM console and select Networking from the "Nano Server Recovery Console"

![](/assets/nano_rc_network.png)

# Assign Variables

The following variables are used throughout this document, please specify the worker node's IP address as well as the password for the local Administrator account.

```
$NanoIP = "169.254.60.172"
$NanoPass = "myPassw0rd"
```

# Copy Files

Use the following commands to copy the diskspd-workernode.ps1 file to the worker node's c: drive.

> Note: PowerShell v5 is reuqired to copy files across a PSSession \(using the -ToSession parameter of Copy-Item\)

```
$s = New-PSSession -ComputerName $NanoIP
Copy-Item -Path .\diskspd-workernode.ps1 -ToSession $s -Destination c: -Force
```

If PowerShell v5 is not available on the control machine, use the following command:

```
Copy-Item -Path .\diskspd-workernode.ps1 -Destination "\\$NanoIP\C$" -Destination c: -Force
```

> Note: The Windows Firewall must be configured ot allow access to the administrative file share on the worker node.

# Register Scheduled Task

Once the first worker node is ready, we can go ahead and register a scheduled task that triggers at boot and starts the diskspd-workernode.ps1 script.

> To get the first nano server's IP address, log into the VMs console.

Use the following PowerShell commands from the control machine, to configure the first worker node:

```
$xml = Import-Clixml .\diskspd-task.xml
$params = @{
    Xml = (Import-Clixml .\diskspd-task.xml);
    CimSession = (New-CimSession -ComputerName $NanoIP);
    TaskName = "diskspd-startup";
    User = "Administrator";
    Password = $NanoPass;
}
Register-ScheduledTask @params
```

