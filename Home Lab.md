Still a WIP!

## Introduction I guess

### What's a home lab
There are several definition of what a home lab is and I'll just go ahead and add mine on the pile. 

A lab in a place to experiment, a place to fail forward. Therefore, broadly, a home lab is a place in your home that you use to research and teach yourself pretty much anything that tickles your interest. I don't know about you, but I'm so vague that for me I could be defining Earth right now. A huge playground.

For tech enthusiasts, their home lab mainly refers to servers, networking, software and security. A place where you can try out new things and learn new technologies or equipment in the comfort of your home.

### But why

![[why-huh.gif]]

My home lab is a place to:
- self-host and own my data
- try, experiment, fail
- test my patience
- contemplate the meaning of life after losing countless hours for a missing character
- lean
- madidate

### How it started

I started coding at an early age. It started with HTML & CSS ("coding"), then some JavaScript and then PHP. I really loved PHP. While EasyPHP wasn't bad, I really wanted to understand how it works and how to set it up **myself**.

![[Pasted image 20230205103031.png]]

 I wanted to upgrade the software versions before EasyPHP would release them. I needed my own Linux Server! I'd find small jobs to earn some money, e.g. mow the lawn, and then spend it all on hardware.

![[serv3.jpg]]
<sup><sub>My Home Lab in 2006 at my parents, I had recently added fans 🤣</sub></sup>

This picture above was taken in 2006 as was one iteration of my first home lab. The left server, using Windows XP, was running the Sphere server powering the small Ultima Online Apocalypse ([uoapo on GH](https://github.com/orditeck/uoapo)) shard for a small community of a hundred players. Truly golden times! I also, at different times, hosted CS1.6 servers, TeamSpeak / Mumble / Ventrilo, Wolfenstein: Enemy Territory, etc.

The right server was running Ubuntu Server and was my first experience with Linux. An incredible love story, much better than any movie one can watch 🤣.

## Hardware

### Proxmox Critical
#### Usage
This machine hosts all the critical parts of our little infra. It uses a low power fanless CPU to stay on as long as possible when running on battery during power outages.

#### Specs:
- Qotom Mini PC Q700G5 Fanless
- NIC: 5x I225-V 2.5G
- CPU: Celeron Quad Core Q750G5 AES-NI
- RAM: 8GB
- SSD: 256GB

#### Cost
$320 brand new from AliExpress in October 2022

---

### Proxmox Lab / Recreational
#### Usage
Host everything that is not critical, doesn't require too much processing power and can be virtualized not to difficultly

#### Specs:
- Lenovo ThinkCentre M710S SFF
- CPU: Core i5-6500
- RAM: 24GB
- SSD: 512GB

#### Cost
$200 reconditioned from Bauer System in February 2022

---

### The Mandatory Window Server
#### Usage
Host anything that is Window-specific and require dedicated processing power

#### Specs
- Dell Precision 3440 SFF
- CPU: Core i3-10100
- RAM: 16GB?
- SSD: 512GB?

#### Cost
$280 brand new from Dell in November 2020

---

### QNAP

---

### Ubiquiti APs

---

### Switches

## Software
Proxmox Lab:
