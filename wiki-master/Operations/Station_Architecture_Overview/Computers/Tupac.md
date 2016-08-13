Tupac is a 2RU Supermicro server. The OS runs off two 64G SATA DOMs plugged directly into the motherboard, configured with a 500M /boot and a 63G / partition, each mdraided.

It has two 1TB SSDs configured as a mirror ZFS zvolume which appears on /data.

The machine has two Gigabit Ethernet NICs and a 10GB fiber NIC. In addition, it has an AudioScience Livewire ASI card.

One ethernet jack will be connected to the Tufts LAN, and the other connected to the internal network. Once the fileserver is migrated to Ballou, the fileserver will be connected via a 10GB SFP+ patch cable to ensure speedy data transfer.

It has redundant hot swap power supplies, and it is also wired for the full 8 disks. Each of the 3.5 bays has been converted to support 2.5 inch drives with associated mounting hardware (this was done to get a cost-effective server with 4 PCIe slots, as opposed to getting a 1RU box.

The machine will not have a WAN IP (so will be accessible only through the firewall through any public server or the NAT router).

See the [reference section on creating guests](https://wiki.wmfo.org/Operations/Reference_and_Hacks/KVM_Guest_Setup) on the machine.

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

-   win10.wmfo.local
-   wmfo-webstream.orgs.tufts.edu
-   wmfo-http.orgs.tufts.edu
-   util.wmfo.local
-   rivendell.wmfo.local
-   scripts.wmfo.local - used to handle routine tasks, scripts, anything remotely bash-y or hack-y, for example automatically propogating SSH keys between all other hosts as one host is updated or propogating emails out of the network etc
