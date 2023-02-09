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
- pfSense (VM)
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
Wi-Fi 6 was an upgrade I was looking forward to and I was not disappointed! One LR AP seems enough for the house. We also have one AP in the shed in repeater/mesh mode as I'm planning to eventually have a smart 240v plug in there to remotely turn on/off the heat.

#### Cost
- AP 6 Long-Range: $250 in January 2022
- 3x AP AC Lite: 
	- 1x $137 in April 2018
	- 1x $118 in June 2019
	- 1x $121 in August 2020

---

### Switches

## Software

I listed pretty much all the software I host on my home lab, but there are some of them that I'd rather take a few more notes about and share a bit more of my experience with them.

### pfSense
I started using pfSense a few years ago when I was looking into a good firewall/router solution to use with custom hardware. I tried OPNsene but didn't find any reason to switch. pfSense does everything I need (and much, much more than I could ever need) and has a wide variety of packages. 

I only use one though: WireGuard. I was previously using OpenVPN but prefers WireGuard.

### Unifi Controller
I don't have much to say here, except that I really like this software. It's easy to use and every upgrade makes it better. Ubiquiti really makes great hardware **and** software. I have two Wi-Fi networks, one for us and one isolated for our guests. I really need to look into having a third for 2.4Ghz smart devices to isolate them from the rest of our network. 

### AdGuard
A must-have, either self-hosted or using their public DNS. 

### Photoprism
I've been contemplating the idea of dropping Google Photos for years now. I used to auto-backup to my NAS all my photos and videos when they were still accessible through Drive, until Google removed that feature on July 2019 in a classic Google move. I didn't bother finding an alternative at that time, but it's been on my mind ever since.

The thing is: Google Photos is darn good. The UI is great, it's easy to share pictures, the partner sharing is extremely useful, the automatic memories/creations are fun. Oh, and its AI recognition is good. Like, scary good. 

Photoprism's face recognition is ages away in comparison. But the reason for that is so obvious that it gave me goosebump when I read it from [their doc](https://docs.photoprism.app/user-guide/organize/people/#asian-faces-and-children):

>It is a known issue that children [...] faces cannot be recognized reliably. 
>
>**The absence of children in the training data comes from the fact that parents do not usually share such images under a public license (and may not have the right to do so).**

How come then that Google Photos' AI is so good? Your guess is as good as mine, and mine would be that they've been using all their users' pictures to train their AI for years. I'm sure they'd say they never did that and never would. And I'm sure I wouldn't believe them.

Moving away from Google Photos is part of a bigger plan to [move away from using Google](From%20the%20Google%20Ecosystem%20to%20kinda%20self-hosted.md) in general.

So I downloaded/exported all my photos from Google using their export tool named [Google Takeout](https://takeout.google.com/), saved them on my QNAP and pointed Photoprism to that folder (readonly for now), then set up a backup job to Wasabi. The first backup took something like a week or two to complete 😬.

My plan was to then remove from Google Photos all my photos and videos taken prior 2023, and re-do the process every year in December. That way I'd still enjoy the easiness of using Google Photos, without keeping almost all my lifetime's memories on that platform.

I haven't done that yet. I was waiting for my first backup to complete before deleting all my data from Google Photos, but then as it took longer than I expected, I kinda moved on to other projects. I'll eventually get back to it, but I also wasn't fully satisfied with Photoprism after playing around a bit with it.

So more to come!

Now I'm diverging from the main subject and hopefully this part will become its own page at some point but I'll note it here for now: I was shocked, and not in a good way, at how many pictures I have.

"Back in the days", we'd have 21 shots and we'd have to pay to get them printed, so they'd better be damn good, right? Today, I just tap tap tap tap that virtual shutter button to make sure I don't miss a good shot. Then I look at the pictures to see if one (or more) are good and move on. I never actually take the time to delete shots that aren't as good and won't be used. They'll eventually just be in the way. But I just left them there. And it was shocking to see how many pictures it ended up being after years of doing that. I'm actually so lazy that I preferred to pay for Google One and get more storage than actually clean up my mess.

### Deluge, Radarr, Sonarr & Jackett


### Web Development & Caddy: 
- Caddy
	- Extensions installed

### WIP
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