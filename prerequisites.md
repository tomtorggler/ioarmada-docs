# Hypervisor

The current version of ioarmada is designed to run on VMware. The environment should be prepared as follows.

## Port Group

A standard or distributed port group is required to provide network connection from the worker nodes to the control machine. As the worker nodes use APIPA addressing, there should be no DHCP service running in that network.

> Use an existing virtual port group or create a new one.

## Datastore

One or more datastores are required to deploy virtual machine to. The datastores where worker nodes will be deployed, are going to expierence some load once the tests are started.

For results to be comparable, each series of tests should be run on datastores using the same storage subsystem. That is, mixing results from an all-flash array with those from an old DAS might not be desirable.

> Use an existing datastore or create a new one.

# Control Machine

A virtual machine running a recent version of Windows Server and PowerShell are required to get the ioarmada up and running.

> PowerShell version 5 is recommended as it makes initial configuration as easy as possible.

## Network

The control machine's network adapter should be connected to the port group created \(or selected\) above. To maintain management access to the control machine, an additional network adapter can be used to connect to the test network.

The worker nodes are configured to connect to the control machine on the IP address: \`169.254.1.1\` so this address has to be configured on the control machines network adapter.

> Add a network adapter and connect it to the virtual port group. Set IP address to 169.254.1.1\/16

## Share

The worker nodes are configured to connect to a share with the name ioarmada on the control machine: \`\169.254.1.1\ioarmada\`.

> Create a folder on the control machine an share it as: ioarmada

## Credentials

In the first version of the ioarmada, the worker nodes and the control machine are not members of a domain. To make configuration as easy as possible, the local administrator account's password is the same on all the machines involved. This might not be an optimal solution from a security point-of-view, but consindering that neither the control machine nor the worker nodes need access to the internet or any production network resources, it is acceptable for now.

> Set the same password for the administrator account on the control machine and the worker node.

# Worker Nodes

The worker nodes are virtual machines running Nano Server TP5 and executing the diskspd run script to actually generate load and measure performance. In this first version, the general idea is to create on worker node, make sure it works as expected and then clone it as many times as your tests require. There are some manual steps required to configure the first node, but once rolled-out, the workers connect to the control machine and update themselves if newer versions of scripts are available.

## Credentials

> Set the same password for the administrator account on the control machine and the worker node.

