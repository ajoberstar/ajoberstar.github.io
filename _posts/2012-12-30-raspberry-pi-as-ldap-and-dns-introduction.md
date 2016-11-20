---
layout: post
title: Raspberry Pi as LDAP and DNS - Introduction
date: 2012-12-30 00:00:00
category: technical
tags:
    - raspberry pi
---
For those of you unfamiliar, [Raspberry Pi](http://www.raspberrypi.org/) is an inexpensive computer that can run Linux and is about the size of a credit card. I think it was primarily designed for educational purposes, to get kids into computers, though it works well for a lot of other use cases. When I got mine, I started off with [Raspbmc](http://www.raspbmc.com/), the XBMC install for the Pi. I had a few issues and decided to stick with my existing Boxee Box for now.

My next project is going to be setting it up as an LDAP server to provide single sign on for my other Linux boxes and maybe trying to connect my Windows boxes to it as well. I'm also thinking about setting up DNS to have intranet domains (e.g. thinking of a .home TLD). I don't know much about configuring either of those or what the implications will be, so this will be a learning process.

I'm starting off by reimaging the Pi with [Raspbian](http://www.raspbian.org/) using the image provided by the [Pi Foundation](http://www.raspberrypi.org/downloads) and these [Linux CLI instructions](http://elinux.org/RPi_Easy_SD_Card_Setup#Copying_an_image_to_the_SD_card_in_Linux_.28command_line.29).

The first part is [DNS and DHCP config](http://www.andrewoberstar.com/blog/2012/12/30/raspberry-pi-as-server-dns-and-dhcp).
