I've been using Home Assistant for years now, and while I have many items on my todolist, I thought I could share what I currently use Home Assistant for and what is my setup.

There are several ways to install Home Assistant and it can be installed on many different type of devices. From my reading on forums, it looks like lot of people install it on a Raspberry Pi. Pis aren't exactly cheap in Canada and they're not that easy to get. I'm also never 100% sure of what my use of Home Assistant would or will be, it's such a powerful piece of software and it has so many cool integrations that I preferred having something a bit too powerful than the contrary. 

Off-lease recondtionned PCs, on the other hands, are easily available. So that's the way I went, and it's pretty much always the way I go when I need a new machine for a project or a server. I highly recommend taking look at the [Bauer Systems Group's Price List](https://docs.google.com/spreadsheets/d/1-hKAmQahPcEV_h5mwflWGLWCQtqkKOBDbsakv4ee2u0) if you're in Canada and are looking for a low-cost option for a small server. I love the Tiny/Micro form factor. SSF is a good size too.

The Home Assistant Operating System (formerly HassOS) can be installed on a lot of hardware, including: 
-   Raspberry Pi
-   Hardkernel ODROID
-   Asus Tinker Board
-   Generic x86-64 (e.g. Intel NUC or any PC really)
-   Virtual appliances

## The hardware

Since the PC I was installing Home Assistant to was, in my opinion, too powerful to only run HA, I went with the latest option from that list: virtual. I like to try to maximize the use of every computer I own, so I installed [Proxmox](https://www.proxmox.com/) and virtualized Home Assistant through a Virtual Machine. 

The host PC specs are:
- CPU: i5-6500
- RAM: 24GB DDR4 (came with 16GB and I had a 8GB stick lying around)
- HDD: 500GB SATA SSD

The VM's spec are:
- CPU: 1 socket, 2 core
- RAM: 4GB
- HDD: 32GB

Then, on the same host, I have Photoprism, Deluge, Sonarr, Radarr, Jackett, Caddy, mailhog, vaultwarden and a container for coding / remote VSCode.

For the sake of closing the Hardware part, I'm going to mention now that I use Zigbee and my main coordinator is plugged through USB on the host and passed down to the VM. I bought a new PoE-powered one though, and I'm very much looking forward to setting it up! It's this one: [SLZB-06 Zigbee Ethernet PoE USB LAN WIFI Adapter](https://smlight.tech/product/slzb-06/) from a small two-persons Ukrainian company founded in 2021 named SMLIGHT. They were procuding their hardware in Kiev but since the war started in Feb 2022, they outsourced the production to China. 