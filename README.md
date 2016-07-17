# Introduction to ioarmada

This books provides documentation for the [ioarmada](https://github.com/tomtorggler/ioarmada "ioarmada on github") project. The project was born out of the need for standardized, comparable performance data, specifically disk subsystem I\/O characteristics.

The project was inspired by the VMFleet, a set of scripts designed to achive the same but focusing on Microsoft's Hyper-V and Storage Spaces Direct solutions. As most of my customers are running VMware vSphere with traditional storage subsystems, a more general approach was required.

# Overview

The main component of the ioarmada is a script that runs on one or more workers and connects to a control machine on a pre-defined IP address. The worker checks the control machine for a "run" script and executes it. The run script contains instructions for DiskSpd which measure I\/O operations on the worker and writes a result back to the control machine. 

In order to spread the loat testing across multiple servers and simulate a situation where multiple VMs are generating load in the environment, the worker node can simply be cloned using the vCenter GUI or PowerCLI tools. 

# DiskSpd

DiskSpd is a storage performance test tool from Microsoft, it is open source software and can be found at the following locations:

GitHub: [https:\/\/github.com\/microsoft\/diskspd](https://github.com/microsoft/diskspd)

Binaries: [http:\/\/aka.ms\/diskspd](http://aka.ms/diskspd "http://aka.ms/diskspd")

# Nano Server

Nano Server is a new, lightweight deployment option of Windows Server 2016 and I thought it would make a good base image for my worker nodes. They don't need a fancy GUI nor many features, all they really do, is running a PowerShell script and diskspd.exe.

More information on Nano Server can be found here: [Getting Started with Nano Server](https://technet.microsoft.com/windows-server-docs/compute/nano-server/getting-started-with-nano-server)



