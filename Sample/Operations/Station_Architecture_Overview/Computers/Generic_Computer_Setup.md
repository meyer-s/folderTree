A few tips on computer setup:

Configure the network interface: call it WMFO LAN and set a static IP address to match the current schema and avoid conflicts.

If you're using a headless host (server without network-manager) use the following /etc/network/interfaces:

    # The primary network interface
    auto eth0
    iface eth0 inet static
            address 192.168.XXX.YYY
            netmask 255.255.0.0
            gateway 192.168.0.10
            dns-nameservers 192.168.0.10
            dns-search wmfo.local

sudo apt-get install git tmux vim openssh-server curl htop

Disable the avahi service daemon to enable .local domain resolution

    Edit /etc/default/avahi-daemon to have 
    AVAHI_DAEMON_DETECT_LOCAL=0

-   Install google-chrome (online download)
-   apt-get install git tmux vim openssh-server curl htop

## SSH Key Setup

-   `ssh-keygen -t rsa`
-   add or update the /etc/hosts file on the router to include your server. You may have to restart dnsmasq to update the changes with `/etc/init.d/dnsmasq restart`
-   `ssh util` and add your device to the `~/.ssh/computers` file (don't copy the key yet)
-   on util, `ssh-copy-id` to your new hostname; verify login works without password
-   on your machine, `ssh-copy-id util` (this will trigger util to copy the updated authorized_hosts file to your device)
-   verify the ~/.ssh/authorized_hosts file is updated on your machine

## Misc
-   mkdir \~/src (for keeping all your source files for things)
-   git clone [https://github.com/WMFO/rivendell.git](https://github.com/WMFO/rivendell.git "https://github.com/WMFO/rivendell.git") (into your \~/src)

 

Follow "For New Installs" on Rivendell if this is to be one of those devices
