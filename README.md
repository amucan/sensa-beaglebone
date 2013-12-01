# sensa-beaglebone

Information and scripts to run Sensa on a BeagleBone board (BBB).

**Table of Contents**
- [Initial setup](#initial-setup)
  - [Angstrom distribution](#angstrom-distribution)
  - [Connection through USB](#connection-through-usb)
  - [Time using ntp](#time-using-ntp)

## Initial setup

### Angstrom distribution

1. Download from: http://beagleboard.org/latest-images
2. Write the image to the SD card.

### Connection through USB

1. If the device `usb0` is not automatically configured, do it directly at the
BBB, through:
  ```
  ifconfig usb0 192.168.7.2
  route add default gw 192.168.7.1
  ```
2. Make sure the host has properly configure the `eth1` network interface.

3. Now you should be able to access from the host through SSH (`ssh
root@192.168.7.2`) or through the browser (http://192.168.7.2).

4. In order to set name servers, put the following on `/etc/resolv.conf`:
  ```
  nameserver 8.8.8.8
  nameserver 4.4.4.4
  ```

To make these changes persistent, use the init script `net-up`:

1. Place the file at `/etc/init.d/`
2. Set execution permissions: `chmod +x /etc/init.d/net-up`
2. Run `update-rc.d net-up defaults`

### Time using ntp
```
ntpdate -b -s -u pool.ntp.org
```
