Util
====

This host runs all the odds and ends services.

* TFTP Server on /tftpboot
* Ubiquiti Unifi AP Software
* SMTP Relay (not yet)


# SSH Key Repository

There is a script in the home directory called `key-update.sh` which is installed on every other server in the station.
It will all the keys over every minute, such that putting your key in util's authorized_keys file will allow you to access every server.
