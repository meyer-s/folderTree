This is a guide for setting up a KVM guest on tupac.

Disk Structure
--------------

/data/vm/{vmname} - one created per VM

/data/vm/{vmname}/disk0 - ZFS block device to hold qcow2 disk image

/data/vm/{vmname}/data - as needed to hold non-OS data. Should be exported over NFS and mounted over network.

To create a zfs subvolume:

zfs create data/vm/blah

To create a 20G block device:

zfs create -V 20G data/vm/blah/etc

Install Guest
-------------

~~~~ {.contents}
virt-install -n nick-test -r 2048 --disk path=/dev/zvol/data/vm/nick-test/disk0,bus=virtio -c ubuntu-14.04.3-server-amd64.iso --network bridge=br1,model=virtio --graphics vnc,listen=0.0.0.0 --noautoconsole -v
~~~~

You can then connect to tupac over VNC to continue with setup.

To start the VM, run:

virsh {vm-name} start

To shut off (not the best choice of vocab):

virsh {vm-name} destroy

Once you're done, you can edit the config file and remove the VNC for this host:

virsh {vm-name} edit

then either shut off and start or do a reload.

### Windows 10 Config

    virt-install -n win10 -r 4096 --vcpus=4 --cpu core2duo --disk path=/dev/zvol/data/vm/win10/disk0,bus=virtio -c /data/iso/en_windows_10_enterprise_version_1511_x64_dvd_7224901.iso --network bridge=br1,model=virtio --graphics vnc,listen=0.0.0.0 --noautoconsole -v

Must select Core2Duo on Win10 or else everything dies. Hopefully this will be fixed soon (it means most likely one of the x86 extensions is causing an invalid instruction...hopefully it's not an important one). 

Need red hat windows virtio driver located in /data/iso/virtio-win-0.1.102.iso

The storage driver is in the iso folder /viostor/{windows-version}/amd64

You'll have to load the storage driver in order to view the disk (otherwise it won't show up). (Virtio is a paravirtualized driver which enables higher throughput.) To do this you will have to click load driver, insert the CD, browse to the folder for your windows version, and load the driver.

To attach a different cdrom while running, use: 

    virsh attach-disk {vm-name} /data/iso/virtio-win-0.1.102.iso  hdc --type cdrom

You will have to reattach the Win10 ISO after you load drivers.

The ethernet virtio driver is in /NetKVM/. This can be installed once the OS is booted but is necessary to conenct to the internet. Navigate to the ethernet device and select update driver, pointing it to the correct one and it should work just fine.

PCIe Passthrough to Rivendell
-----------------------------

See [this article on PCI passthrough](https://www.suse.com/documentation/sles11/book_kvm/data/sec_libvirt_config_pci_virsh.html "https://www.suse.com/documentation/sles11/book_kvm/data/sec_libvirt_config_pci_virsh.html").

    03:00.0 PCI bridge: Texas Instruments XIO2001 PCI Express-to-PCI Bridge
    04:00.0 Multimedia audio controller: Texas Instruments TMS320C6414 TMS320C6415 TMS320C6416

Those are the two devices (I think), with IDs:

    03:00.0 0604: 104c:8240
    04:00.0 0401: 104c:a106

Essentially you \_should\_ just be able to add the following XML to the machine:

    <hostdev mode='subsystem' type='pci' managed='yes'>
          <source>
            <address domain='0x0000' bus='0x04' slot='0x00' function='0x0'/>
          </source>
          
        </hostdev>    

Make sure to get bus and slot correct. You'll want to do a \`virsh nodedev-dumpxml DEVICE\` on the pci device in question to find those entries. See the link above, but they're taken off the lspci entries.

And KVM will add in another line in the blank one:

    <address type='pci' domain='0x0000' bus='0x00' slot='0x07' function='0x0'/>

and then start the machine. The important configurations on the host are the intel\_iommu=on in the grub command line and the vfio-pci module.

Note that pci-stub is deprecated though there are still some references online to it.

You[cannot attach the PCI adapter device](https://lists.nongnu.org/archive/html/qemu-devel/2016-02/msg05734.html "https://lists.nongnu.org/archive/html/qemu-devel/2016-02/msg05734.html").

 

1.  1. [Disk Structure](#Disk_Structure)
2.  2. [Install Guest](#Install_Guest)
    1.  2.1. [Windows 10 Config](#Windows_10_Config)

3.  3. [PCIe Passthrough to Rivendell](#PCIe_Passthrough_to_Rivendell)

