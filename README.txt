Two-Tier Leaf and Spine Topology with BGP as the IGP
====================================================

This document explains how to use the available code to create a Two-Tier Leaf and Spine Topology with BGP as the IGP.


Pre-requisites
==============

This setup was tested on Ubuntu 16.04 software(Desktop version) and requires the below software to be installed in the Server.

1.Vagrant ( Version 1.9.5 or above)
2.Ansible ( Version 2.8.5 or above)

Vagrant is used to create the Virtual Machines.The individual nodes in this topology which are the leafs,spines and servers will be individual virtual machines.
Ansible is a Devops tool which is used to configure the network device.

Below are some other requirements/recommendations
1.If you wish to run this setup please note that running this simulation uses more than 8G of RAM.
2.The Ansible is installed in the host machine itself and not on a separate virtual machine.So configuration is to be done in such a way that the Ansible in the host can connect the individual virtual machines and configure it.
3.Download the "cumulus-linux-3.7.6-vx-amd64-vbox.box" software or any other higher version and place it in the "vagrant_files" directory after the git clone is made.

Topology and other configuration related files
==============================================
1.The topology which is used for this setup is provided in the topology.jpg file.
2.The excel file Topology_ls_1.xls has the details used to bring-up the vagrant and the BGP.
3.The configuration of individual routers are provided in the configuration.txt file.

Details
=================
1.Download the software from the github and untar it or you can git clone it to the server where you want to deploy this configuration.

2.Create the topology using the command "vagrant up".While the VMs are booted make a note of the SSH port number allocated for each VM as this will be required for Ansible host file configuration.

For example below is the SSH port number allocated for Spine1
Spine1: SSH address: 127.0.0.1:2222

You can also get this information using the command "sudo lsof -i -n | grep VBoxHeadl"

3.Open the "hosts" file in the directory and check if the noted port numbers in the step 2 are correct.If there is any discrepancy then update it.

4.The twotierls.yml is the main playbook which is used to bring-up the entire topology.

Run the playbook with the below command,

sudo ansible-playbook twotierls.yml

Sometimes the you might get the error in configuring the Server and under that condition re-run the playbook.

5.To verify if everything is working properly,log into the Servers and ping each other.

vagrant@server1:~$ ping 10.3.20.1
PING 10.3.20.1 (10.3.20.1) 56(84) bytes of data.
64 bytes from 10.3.20.1: icmp_seq=1 ttl=61 time=3.52 ms
64 bytes from 10.3.20.1: icmp_seq=2 ttl=61 time=3.75 ms

vagrant@server2:~$ ping 10.1.20.1
PING 10.1.20.1 (10.1.20.1) 56(84) bytes of data.
64 bytes from 10.1.20.1: icmp_seq=1 ttl=61 time=3.68 ms
64 bytes from 10.1.20.1: icmp_seq=2 ttl=61 time=3.55 ms

If both the servers are able to communicate with each other then execution of the script has taken place successfully.

6.In order to understand the configuration,log into each of the VM and explore the configuration.

For instance to see the bgp configuration of Leaf1,

vagrant ssh Leaf1
sudo vtysh (to get into the FRR shell)

leaf1# show bgp summary

IPv4 Unicast Summary:
BGP router identifier 10.254.0.1, local AS number 64513 vrf-id 0
BGP table version 8
RIB entries 15, using 2280 bytes of memory
Peers 2, using 39 KiB of memory
Peer groups 1, using 64 bytes of memory

Neighbor        V         AS MsgRcvd MsgSent   TblVer  InQ OutQ  Up/Down State/PfxRcd
spine1(swp2)    4      64500     247     248        0    0    0 00:11:53            5
spine2(swp3)    4      64500     247     247        0    0    0 00:11:53            5

Total number of neighbors 2

IPv6 Unicast Summary:
BGP router identifier 10.254.0.1, local AS number 64513 vrf-id 0
BGP table version 0
RIB entries 0, using 0 bytes of memory
Peers 2, using 39 KiB of memory
Peer groups 1, using 64 bytes of memory

Neighbor        V         AS MsgRcvd MsgSent   TblVer  InQ OutQ  Up/Down State/PfxRcd
spine1(swp2)    4      64500     247     248        0    0    0 00:11:53            0
spine2(swp3)    4      64500     247     247        0    0    0 00:11:53            0

