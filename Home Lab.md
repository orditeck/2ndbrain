Still a WIP!

## Introduction I guess

### What's a home lab
There are several definition of what a home lab is and I'll just go ahead and add mine on the pile. 

A lab is a place to experiment, a place to fail forward. Therefore, broadly, a home lab is a place in your home that you use to research and teach yourself pretty much anything that tickles your interest. I don't know about you, but I'm so vague that for me I could be defining Earth right now. A huge playground.

For tech enthusiasts, their home lab mainly refers to servers, networking, software and security. A place where you can try out new things and learn new technologies or equipment in the comfort of your home.

### But why
![[why-huh.gif]]

My home lab is a place to:
- self-host and own my data
- have fun while learning
- try, experiment, fail
- test my patience and contemplate the meaning of life after losing countless hours for a missing character in a config file

### How it started

I started coding at an early age by reading online and self teaching myself. It started with HTML & CSS ("coding"), then some JavaScript and then PHP. I really loved PHP. While EasyPHP wasn't bad, I really wanted to understand how it works and how to set it up **myself**.

![[Pasted image 20230205103031.png]]

 I wanted to upgrade the software versions before EasyPHP would release them. I needed my own Linux Server! I'd find small jobs to earn some money, e.g. mow the lawn, and then spend it all on hardware.

![[serv3.jpg]]
<sup><sub>My Home Lab in 2006 at my parents, I had recently added fans 🤣</sub></sup>

This picture above was taken in 2006 as was one iteration of my first home lab. The server on the left, under Windows XP, was running the Sphere server powering the small Ultima Online Apocalypse ([uoapo on GH](https://github.com/orditeck/uoapo)) shard for a community of a hundred players. Truly golden times! I also, at different times, hosted CS1.6 servers, TeamSpeak / Mumble / Ventrilo, Wolfenstein: Enemy Territory server, etc.

The PC on the right was running Ubuntu Server and was my first experience with Linux. An incredible love story, much better than any movie one can watch 🤣. It was primarily a public web server to host my small project, like Orkïka, a text-based web-browser medieval game written in PHP.

## Hardware

### Proxmox Critical
![[Pasted image 20230205113019.png]]
#### Usage
This machine hosts all the critical parts of our little infra. It uses a low power fanless CPU to stay on as long as possible when running on battery during power outages.

It runs Proxmox and runs only three services:
- OPNsense (VM)
- Unifi Controller
- AdGuard

#### Specs
- Qotom Mini PC Q750G5-S08 Fanless
- NIC: 5x I225-V 2.5G
- CPU: Celeron J4125 Quad Core, 2.0GHz, Up to 2.7GHz, 4M Cache, 10W TDP
- RAM: 8GB
- SSD: 256GB

#### Cost
$320 brand new from AliExpress in October 2022

---

### Proxmox Lab / Recreational
![[Pasted image 20230205113735.png]]
#### Usage
Host everything that is not critical, doesn't require too much processing power and can be virtualized not to difficultly.

It runs Proxmox and run these services:
- **Photoprism**: AI-Powered Photos App for the Decentralized Web
- **Deluge**: torrent client
- **Radarr**: movie collection manager 
- **Sonarr**: software-based Personal Video Recorder (PVR) for TV shows
- **Jackett**: API Support for your favorite torrent trackers
- Barebone **Ubuntu Server** used as web server (Remote-SSH VSCode)
- **Caddy**: powerful, enterprise-ready, open source web server with automatic HTTPS written in Go
- **Mailhog**: email testing tool for developers
- **Vaultwarden**: Alternative implementation of the [Bitwarden](https://bitwarden.com/) server API written in Rust and compatible with upstream Bitwarden clients
- **[[Home Assistant - How I use it and for what|Home Assistant]]**

#### Specs
- Lenovo ThinkCentre M710S SFF
- CPU: Core i5-6500
- RAM: 24GB
- SSD: 512GB ADATA SU760

#### Cost
$200 reconditioned from Bauer System in February 2022

---

### The Mandatory Window Server
![[Pasted image 20230205113445.png]]
#### Usage
Host anything that is Window-specific and require dedicated processing power.

It runs Windows 11 and run these services:
- Blue Iris: video security software that provides recording and playback for up to 64 IP network cameras or webcams
- Plex Media Server: the one place to find and access all our TV shows and movies

#### Specs
- Dell Precision 3440 SFF
- CPU: Core i3-10100
- RAM: 24GB
- SSD: Crucial P2 500GB PCIe
- HDD: Western Digital 3TB WD Red Plus NAS

#### Cost
$280 brand new from Dell in November 2020

---

### QNAP
![[Pasted image 20230205113100.png]]
#### Usage
Network Attached Storage (NAS): a storage that's available to all devices on the network.

I keep it very barebone as it's not a powerful machine.

Divided in two volumes:
1. Family (4TB)
	- Photos
	- Documents
	- Syncthing directories
2. Stuff (12TB)
	- Torrents
	- Security Cameras recordings
	- Proxmox backups

Apps installed:
- [Syncthing](https://syncthing.net/) installed through the QPKG Store. It is a continuous file synchronization program. It synchronizes files between two or more computers in real time, safely protected from prying eyes.

Off-site backups:
- To Wasabi (S3-like) for all important data.
- Also a real-time sync with Google Drive for my daily Syncthing directory for convenience, but that's something I'm aiming to remove in the near future since I haven't used Google Drive for ages.

#### Specs
- Model: TS-431P
- CPU: ARM Cortex-A15 CPU @ 1.70GHz 
- RAM: 1GB DDR3
- Disks: 
	- 2x 4TB RAID 1, Encrypted
	- 2x 12TB RAID 1, Non Encrypted

#### Cost
- QNAP: $245 from Amazon in June 2018
- 2x 4TB disks: 205$ from Amazon in March 2022 as one of the old drive started to fail S.M.A.R.T. tests.
- 2x 12TB disks: $575 from BestBuy in February 2021, shucked from WD easystore 12TB USB 3.0 Desktop External Hard Drive (WDBAMA0120HBK-NESN)

---

### Ubiquiti APs
![[Pasted image 20230205120806.png]]

#### Usage
Wi-Fi!

#### Cost
- Access Point WiFi 6 Long-Range: $250 in January 2022
- 3x Access Point AC Lite: 
	- 1x $137 in April 2018
	- 1x $118 in June 2019
	- 1x $121 in August 2020

---

### Switches

## Software

- OPNsense
- Unifi Controller
- AdGuard
- Photoprism
- Deluge, Radarr, Sonarr & Jackett
- Web Development & Caddy: 
	- Caddy
		- Extensions installed
	- minio
	- PGAdmin
	- redis
	- MariaDB
	- CodeServer
	- pm2
	- nginx
	- php
- Mailhog
- Vaultwarden
- [[Home Assistant - How I use it and for what|Home Assistant]]
- Blue Iris
- Plex Media Server
- Syncthing