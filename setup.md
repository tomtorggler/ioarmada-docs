# Create Nano Server Image

To create a Nano Server Image, see: [Appendix: Create Nano Server Image](/appendix-create-nano-server-image.md)

# Scale

The following PowerCLI commands can be used to clone the VM.

```
PowerCLI C:\> $vm = Get-VM ioarmada0
PowerCLI C:\> 1..8 | % {New-VM -VM $vm -Name "ioarmada0_$_" -ResourcePool Resources -Datastore MARVIN-Virtual-SAN-Datastore-0105df5c-40c5-47da-a7f1-c135da25ee0f} | Start-VM
```

