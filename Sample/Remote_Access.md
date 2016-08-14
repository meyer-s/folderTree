# WMFO Remote Access

Here's how to access the station remotely.

## Website

The linode host can be accessed at `wmfo-linode.wmfo.org`, using the Linux credentials.

## Station Devices

WMFO has a LAN using RFC1918 addresses in the 192.168.0.0/16 subnet. This subnet is not accessible directly from the internet due to RFC1918.

### Servers

Several computers have connections to both the LAN and the internet:

1. wmfo-http.orgs.tufts.edu - web host
2. wmfo-webstream.orgs.tufts.edu - Windows webstream host
3. wmfo-primary.orgs.tufts.edu - old primary router.
4. wmfo-secondary.orgs.tufts.edu - secondary tower router, now used for most traffic

Once on these hosts you may connect to LAN devices. Those may all be accessed directly using RDP for windows on port 9636 or Linux SSH on port 2234. The routers, in addition to the SSH CLI, have SSLed Web Interfaces accessible externally as well.

wmfo-http requires an SSH key and will not accept password authentication.

webstream host: be very careful RDPing in. If you must, please ensure you've disabled the Audio forwarding (select "Play on remote host") or else it will mess with audio settings.

wmfo-gm.orgs.tufts.edu host (from above) is accessible directly through Curtis Hall and is located in the GM office.

### Internal Devices

Your best bet for accessing the station's many many devices which don't have full internet routing is to log in using Windows RDP. There are available Remote Desktop Connections for Windows (should be included) as well as OSX (app store). RDP requires Network Level Authentication (NLA).

If the station doesn't have full power, this is a bit of a cat and mouse game. wmfo-gm is available in Curtis. Win10 goes through the Ballou router.

win10 host: Log in with Windows credentials to lan.wmfo.org port 9638.

### Alternate Route

lan.wmfo.org refers to the wmfo-secondary.orgs.tufts.edu router in Ballou. Over HTTPS, it uses the standard Linux credentials. Port forwarding is set up:

SSH:

- Adele (studio a) - port 2234
- Carlos (studio c) - 2235
- Util (sandbox server) - 2241
- Ringo (fileserver) - 2239
- Elvis (backup fileserver) - 2238
- Tupac (hypervisor) - 2236
- Rivendell - 2237

Other:

- win10 RDP 9638

See the lan.wmfo.org router config on NAT forwarding for all ports.

#### SOCKS

ssh wmfo-admin@lan.wmfo.org -p 2234 -D 8888

Once authenticated, use FoxyProxy with Chrome to redirect to the localhost:8888 port. All traffic in Chrome will pass through the router.

ssh -X will enable X forwarding.
