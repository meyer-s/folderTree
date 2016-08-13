Functionality
-------------

Supertramp hosts DNS and Samba shares for the station.

### Samba

Configured through /etc/samba/smb.conf, this exposes the fileshares for Rivendell, importing, and backup. User management for Samba is separate from Linux login, and you should create users on Linux with /bin/nologin as their shell and then add them to Samba with the smbpasswd command. Names should be all lowercase, as login names are sent typically in all caps to the auth server and then the Samba server typically tries a few capitalization combinations (the first being all lower case). The shares themselves are currently on the NTFS RAID which will be moved to a Linux FS when we build the next tower server.

Samba permissions are annoying as all hell because Windows permission model is different than Unix. It's currently setup with 775 permissions and mounted as rivendell:sambashare and every user who uses a share is added to the sambashare group. Permissions can then be controlled fully within smb.conf giving flexibility to make certain shares read only etc.

#### Upgrades

Be careful when running \`apt-get upgrade\` because when Samba upgrades it kills the shares and, by extension, Rivendell playback. As long as no playback is happening, you should be fine to upgrade and the shares should restore when Samba comes back online. If it doesn't, try un+re mounting the share on Duke with:

    # umount /var/snd
    # mount /var/snd

(\# means root, so use \`sudo\` or \`sudo -s\`)

Mounting Elsewhere

Typically shares are mounted by setting them up in /etc/fstab, shown here mounting Smooth shares on Super over the dedicated interserver link:

    \\10.0.4.210\Rivendell-Smooth /mnt/smooth/Rivendell cifs noauto,dir_mode=0775,file_mode=0775,credentials=/etc/smbcred,_netdev,sec=ntlm 0 0

    \\10.0.4.210\tobeImported-Smooth /mnt/smooth/tobeImported cifs noauto,dir_mode=0775,file_mode=0775,credentials=/etc/smbcred,_netdev,sec=ntlm 0 0

    \\10.0.4.210\Archive-Smooth /mnt/smooth/Archive cifs noauto,dir_mode=0775,file_mode=0775,credentials=/etc/smbcred,_netdev,sec=ntlm 0 0

 

Credentials should be placed in /etc/smbcred:

    username=nick
    password=daspasswd

They can then be mounted and unmounted easily (as root):

    ​# mount /mnt/smooth/Rivendell
    # umount /mnt/smooth/Rivendell

#### Backups

Backups are accomplished through rsync. The secondary Super shares are mounted in /mnt/super/.

### DNS

Runs through Bind9, configured in /etc/bind. The primary issue is getting syntax right. It took many hours to set up.

### DHCP

Ideally DHCP will move to this box to unify DHCP and DNS and give more configurability. We could also switch units to all use DHCP, thus enabling easy reconfiguration of addresses and DNS.

History
-------

This machine ran Windows Server 2008 until the great server crash of May 2014 when it was rebuilt to fulfill the previous server role without documentation by Nick in two days of pain and suffering.

Be careful which plugs you pull when.

1.  1. [Functionality](#Functionality)
    1.  1.1. [Samba](#Samba)
        1.  1.1.1. [Upgrades](#Upgrades)
        2.  1.1.2. [Backups](#Backups)

    2.  1.2. [DNS](#DNS)
    3.  1.3. [DHCP](#DHCP)

2.  2. [History](#History)

