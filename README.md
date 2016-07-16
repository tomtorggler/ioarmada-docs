# Introduction to ioarmada

This books provides documentation for the [ioarmada](https://github.com/tomtorggler/ioarmada "ioarmada on github") project. The project was born out of the need for standardized, comparable performance data, specifically disk subsystem I\/O characteristics.

The project was inspired by the VMFleet, a set of scripts designed to achive the same but focusing on Microsoft's Hyper-V and Storage Spaces Direct solutions. As most of my customers are running VMware vSphere with traditional storage subsystems, a more general approach was required.

# Overview

The main component of the ioarmada is a script that runs on one or more workers and connects to a control machine on a pre-defined IP address. The worker checks the control machine for a \_run\_ script and executes it. The run script contains instructions for DiskSpd which measure I\/O operations on the worker and writes a result back to the control machine.

# DiskSpd

DiskSpd is used 

# Nano Server



