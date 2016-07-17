# Create Nano Server Image

To create a Nano Server Image, see: [Appendix: Create Nano Server Image](/appendix-create-nano-server-image.md)

# Prepare Control Machine

On the control machine install PowerShell version 5 \(if not already installed\). The required WMF5 packet can be downloaded here: https:\/\/www.microsoft.com\/en-us\/download\/details.aspx?id=50395



# Register Scheduled Task

Once the first worker node is ready, we can go ahead and register a scheduled task that triggers at boot and starts the diskspd-workernode.ps1 script.

> To get the first nano server's IP address, log into the VMs console.

Use the following PowerShell commands from the control machine, to configure the first worker node:

```
$xml = Import-Clixml .\diskspd-task.xml
$cs = New-CimSession -ComputerName "Nano Server IP"
$password = "notSoSecure"
Register-ScheduledTask -Xml $xml -CimSession $cs -TaskName diskspd-startup -User Administrator -Password $password
```

