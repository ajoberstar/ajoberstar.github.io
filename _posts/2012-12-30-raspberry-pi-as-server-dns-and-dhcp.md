---
layout: post
title: Raspberry Pi as Server - DNS and DHCP
date: 2012-12-30 01:00:00
category: technical
tags:
    - raspberry pi
---
In my [previous post](http://www.andrewoberstar.com/blog/2012/12/30/raspberry-pi-as-ldap-and-dns-introduction), I mentioned I'm trying to set up my [Raspberry Pi](http://www.raspberrypi.org/) as an LDAP and DNS server.

Once I got Raspbian installed, I started to look into setting up the DNS server, the end goal is to have domain names for all devices on my internal network (e.g. instead of `192.168.0.5`, I can use `mydevice.lan.mydomain.com`). While, you can do this with platform specific hostname files (e.g. `/etc/hosts` or `C:\Windows\system32\drivers\drivers\etc\hosts`), it requires you to maintain that file on each device.

The final process I went through isn't Raspberry Pi specific, it should work on at least any Debian-based system.

I would also like to preface this by saying I am not a networking expert, so this post reflects my layman's understanding of what I ended up configuring

## DNS Software

I've looked into setting up internal DNS before and always ended up finding instructions for [bind](https://www.isc.org/software/bind). From what I can tell, bind is insanely powerful, but it's also crazy complicated. For the tiny use case I have, the configuration is too much overhead.

I ended up finding references to [dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html), which is purpose built for small networks. Here's a rundown of the basic functionality I ended up using:

* **DNS forwarding and cache** -  You still use your existing DNS (be it your ISP's DNS, Google public DNS, or OpenDNS) for accessing the Internet. In theory, the caching it provides could increase performance, though I don't have any expectations about that.
* **DNS for static IPs** - Define domain names for devices with static IPs on your network.
* **DHCP** - General DHCP provider.
* **DNS for DHCP clients** - For any client that leases an IP from dnsmasq, it will also provide a domain name to that IP. Essentially your own internal dynamic DNS.

I wasn't interested in moving DHCP from my router to the Pi, until I found out that my router ([Asus RT-N66U](http://www.asus.com/Networks/Wireless_Routers/RTN66U/)) also uses dnsmasq for DHCP. I was able to telnet onto the router to see the config, but I noticed a few options I wanted to set were not turned on and there wasn't a way to configure them from the web UI. While I could modify the config file manually, it is overwritten at restart by the stock firmware. So back to installing on the Pi.

## Picking Internal Domain Names

I started out planning to pick some TLD not used by ICANN (e.g. `.local` or `.home`) for my internal domains. Most posts I read on this subject recommended against that in case ICANN decided to use it in the future. Honestly, I don't expect that to be an issue, but I followed their advice anyway.

The recommendation was to stick with a domain you already own and designate a subdomain for all of your internal hosts to be assigned under. For example, if you own `mydomain.com`, you could designate `lan.mydomain.com` to be the root for all of your internal domains. A device might then be assigned `mydevice.lan.mydomain.com`. Gets a little wordy, but at least the namespace is safe.

## Installation

Through the magic of Debian, installing dnsmasq is as simple as:

    sudo apt-get install dnsmasq

## Configuration

For my setup, dnsmasq configuration happens in the following files:
* `/etc/dnsmasq.conf` - dnsmasq specific configuration
* `/etc/resolv.conf` - DNS to forward to (and the one used by the server running dnsmasq)
* `/etc/hosts` - host names for static IPs
* `/etc/ethers` - manually assigned IPs specified as MAC to IP mappings (optional)

### /etc/dnsmasq.conf

This configures how the DNS server and the DHCP provider (if enabled) should behave. I'll discuss the main options I used, but the example configuration file provided with the install has good documentation.

Some domain lookups are essentially guaranteed to come up empty on the wider Internet. You can disable forwarding of them with the following lines:

    # won't forward unqualified names (e.g. myserver)
    domain-needed

    # won't forward some non-routed addresses
    bogus-priv

    # won't forward requests for your intranet subdomain
    local=/lan.mydomain.com/

That last one is key. It forces that subdomain to be resolved only via internal config: the hosts file or DHCP clients.

To specify the root subdomain for your intranet, use the following two options:

    # append the domain (below) to all hosts in the hosts file
    expand-hosts

    # appended to DHCP hosts and, if above option specified, to hosts from static IPs
    domain=lan.mydomain.com

If you want to use the `/etc/ethers` file (see section farther down) add this option:

    read-ethers

The rest is DHCP config. I copied it from my router's dnsmasq config, so I don't know much about all of the options.

**NOTE:** If you do enable DNS via dnsmasq, you should shut off the DHCP on your router. After an IP refresh, your DHCP clients should all work fine.

### /etc/resolv.conf

In my network, this points to my router. I would expect that is the normal setup, but your mileage may vary. The file's only contents are the IP of the DNS server to point to.

### /etc/hosts

You'll want to leave the existing contents, but add the host names for any of your devices using static IPs. You do not need every device listed in here, just the ones you want to be addressable via a domain name.

Format is `<IP> <host name>`, and the host name should only be the lowest level qualifier of the host (not the full domain name). For example, if you want a device to be `mydevice.lan.mydomain.com`, only specify `mydevice`.

    192.168.1.301 mynas
    192.168.1.302 webserver

### /etc/ethers

This is only needed if you have a few devices you want to assign static IPs to, but can't or don't want to configure the static IP on the devices themselves.

This is simply a `<MAC> <IP>` formatted file, with one mapping per line, for example:

    00:00:00:00:00:00 192.168.0.200
    00:00:00:00:00:01 192.168.0.201

## Final Thoughts

As neat as it is, the benefits of domain names internally are pretty minimal. I already had the handful of static IPs I use memorized, but it will be nice to have a friendlier name to use. I do like having domains for the DHCP clients, however, since it removes the need to look up the IP beforehand.

Next step will be setting up LDAP on the Pi.
