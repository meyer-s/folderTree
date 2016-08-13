# WMFO Servers

# Tupac

Tupac is a 2RU Supermicro server. The OS runs off two 64G SATA DOMs plugged directly into the motherboard, configured with a 500M /boot and a 63G / partition, each mdraided.

It has two 1TB SSDs configured as a mirror ZFS zvolume which appears on /data.

The machine has two Gigabit Ethernet NICs and a 10GB fiber NIC. In addition, it has an AudioScience Livewire ASI card.

One ethernet jack will be connected to the Tufts LAN, and the other connected to the internal network. Once the fileserver is migrated to Ballou, the fileserver will be connected via a 10GB SFP+ patch cable to ensure speedy data transfer.

It has redundant hot swap power supplies, and it is also wired for the full 8 disks. Each of the 3.5 bays has been converted to support 2.5 inch drives with associated mounting hardware (this was done to get a cost-effective server with 4 PCIe slots, as opposed to getting a 1RU box.

The machine will not have a WAN IP (so will be accessible only through the firewall through any public server or the NAT router).

See the [reference section on creating guests](https://wiki.wmfo.org/Reference/KVM_Guest_Setup) on the machine.

## Networking

The network is configured with bridges. [This is a good overview](http://www.microhowto.info/troubleshooting/troubleshooting_ethernet_bridging_on_linux.html) of bridge troubleshooting using the `brctl` command.

- em1 is the WMFO LAN connection into the cisco switch
- br1 is the bridge to the WMFO LAN and has the primary IP assigned to it. Each VM attaches to this bridge for WMFO LAN connectivity.
- em2 is the TUFTS WAN connection into the data jack positioned 10 meters from the computer over the door
- br2 is the Tufts bridge etc.
- vmnet0, vmnet1... are the KVM machines' interfaces

You can view all this using the `ip link show` command.

Note that we had an issue with the br2 not coming up automatically at boot. It can be brought up manually with `ip link set br2 up` and then it works AOK. The hosts connected to br2 will fail to autostart if this happens. We may resolve this with a script.

`brctl show` will list the bridge interfaces and which are connected together.

Guests

## win10.wmfo.local (tupac vm)

This host runs all miscellaneous scripts. It has VNC and Putty with Pagent and keys all set up, as well as Firefox and Java for remote administration of all annoying Java Applets.

## wmfo-webstream.orgs.tufts.edu (tupac vm)

This host runs the [webstream](https://wiki.wmfo.org/Reference/Webstream/). It does so off an AoIP Driver License (4x4 channels). Could support other services utilizing this license.

## wmfo-http.orgs.tufts.edu (tupac vm)

## util.wmfo.local (tupac vm)

* SSH key distributor
* Repositories

## rivendell.wmfo.local (tupac vm)

## ringo.wmfo.local

Ringo is the primary file server for WMFO.

The main RAID is installed on top of 8x6TB WD Red drives. These are all grouped under a single RAIDZ pool using the ZFS filesystem.

Ringo's primary duty is to expose network fileshares:

-   Rivendell: mounted only on rivendell share
-   tobeImported: mounted on Floodland for ripping and Duke for import
-   Backup: mounted on Duke and Devolution for backups

Fileshares can be exposed from within ZFS in either Samba or NFS, NFS being preferred for Linux clients and Samba required for Windows.

Ringo has an IPMI interface (ringo-ipmi.wmfo.local) for out of band reboots and an external NIC. 

Ringo also manages backups.
