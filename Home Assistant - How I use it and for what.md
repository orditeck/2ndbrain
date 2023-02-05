![Relative date](https://img.shields.io/date/1675563553?color=3482cc&label=📅%20Last%20updated)

I've been using Home Assistant for years now, and while I have many items on my todolist, I thought I could share what I currently use Home Assistant for and what is my setup. I tried several integrations and devices through the years. Some I came to love, some to forget, some to regret and finally, some to heartfully hate (looking at you, Tuya).

![[hasetup.png]]
<sup><sub>The Thing / Main Controller / Smart Hub / Keven hasn't named me 😢</sub></sup>

But even after a few years of use, I feel like I'm still an amateur user. Home Assistant has so many features and so so many integrations to play with!

Home Assistant can be very intimidating at the beginning. I wasn't that used to the YAML syntax and there was a bit of a learning curve there but I quickly started to like it. What's not to love in being able to manage my automations in VSCode. I'm sure there's an amazing UI for it in HA by now but nope thanks, I'm YAML team!

But yeah, reading about all the automations, the devices, the protocols, the configurations, it can quickly be overwhelming. If you're looking to getting started but feel overwhelmed, just do it! It gets quickly very addictive 😃.

![[Pasted image 20230204175453.png]]

## My setup
There are several ways to install Home Assistant and it can be installed on many different type of devices. From my reading on forums, it looks like lot of people install it on a Raspberry Pi. Pis aren't exactly cheap in Canada and they're not that easy to get. I'm also never 100% sure of what my use of Home Assistant would or will be, it's such a powerful piece of software and it has so many cool integrations that I preferred having something a bit too powerful than the contrary.

Off-lease reconditioned PCs, on the other hands, are easily available. So that's the way I went, and it's pretty much always the way I go when I need a new machine for a project or a server. I highly recommend taking look at the [Bauer Systems Group's Price List](https://docs.google.com/spreadsheets/d/1-hKAmQahPcEV_h5mwflWGLWCQtqkKOBDbsakv4ee2u0) if you're in Canada and are looking for a low-cost option for a small server. I love the Tiny/Micro form factor. SSF is a good size too.

The Home Assistant Operating System (formerly HassOS) can be installed on a lot of hardware, including:
-   Raspberry Pi
-   Hardkernel ODROID
-   Asus Tinker Board
-   Generic x86-64 (e.g. Intel NUC or any PC really)
-   Virtual appliances

## The hardware
### Server
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

For the sake of closing the Hardware part, I'm going to mention now that I currently use Zigbee with the main coordinator plugged through USB on the host and passed down to the VM. It'll change soon though since I bought a new PoE-powered one, and I'm very much looking forward to setting it up! It's this one: [SLZB-06 Zigbee Ethernet PoE USB LAN WIFI Adapter](https://smlight.tech/product/slzb-06/) from a small two-persons Ukrainian company founded in 2021 named SMLIGHT. They were producing their hardware in Kiev but since the war started in Feb 2022, they outsourced the production to China.

### Clients
We used Home Assistant mainly through the Hub (picture at the top of the page) but also on our phones and smart watches.

## The integrations / smart devices / services

- ESP32 to track BLE devices:
	- Xiaomi thermometers (LYWSDCGQ & LYWSD03MMC): temperature, humidity
	- HHCC Flower Monitor (HHCCJCY01): temperature, moisture, ambient light and nutrient levels in the soil
- zigbee2mqtt: more about my zigbee affection here. Current devices:
	- Smart Deadbolt (Schlage)
	- Roller blind motor (Generic TuYa TS0601 from AliExpress)
	- Motion Sensor (Aqara RTCGQ11LM)
	- Door Sensor (Aqara MCCGQ11LM)
	- Smart siren / alarm (HEIMAN HS2WD-E)
	- Bunch of smart bulbs
		- TuYa TS0505B
		- Sengled Zigbee Smart Light Bulbs
- HACS: awesome tool
- Tuya: I have a few WiFi smart bulbs and plugs that I bought on AliExpress. I don't like devices that use Tuya (more about that [here](#tuya)) and I'm slowly moving away / replacing them for Zigbee devices. Real bummer since I invested quite a lot of money in these WiFi devices when I started getting into smart devices.
- localtuya: After my experience with Tuya, I decided to try out localtuya and it works well! I moved a few devices to it but I ended up switching to Zigbee so that's still a WIP.
- Midea Aircon: allows us to control my Senville heat pump through HA.

## What I particularly like
There's a lot I like about my Home Assistant setup, but here are the highlights.

### My favorite automations and features
1. The smart lock unlocks the door at set times, e.g. when the kids are expected to come back from school. They don't need a key, and they can't lose a key they don't have.
2. Smart Speakers tell the kids to get ready for school and to leave at specific them so we don't have to watch the time. A bit earlier in the winter because it takes longer to get dressed vs spring/autumn. Eventually I'd like to take the weather into consideration to dynamically remind them, for example, to bring a rain coat because it might rain on the way back.
3. The kids' light turn on automatically at set time in the morning to let them know they can get up. If the light isn't on, it means it's still time to sleep! Remarkably useful. They also turn off automatically around 8AM since they're not needed anymore and turned back on in the evening. We currently turn them off "manually (OK Google!)" after kissing them goodnight.
4. The door automatically unlocks for my wife and I when we approach the house and we get a notification on our watch to let us know that it's now unlocked.
5. The lights change based on the sun position, which is used to calculate the color temperature and brightness that is most fitting for that time of the day. Scientific research has shown that this helps to maintain your natural circadian rhythm (your biological clock) and might lead to improved sleep, mood, and general well-being. And let me tell you that it does for us!
6. When away, if the door is unlocked/opened, I get an instant notification on my phone with a picture from the main entrance's camera.
7. When away, I can unlock the door remotely. It's been hugely helpful, for example when we were 200km away for my wife's birthday and one of her friend didn't let me know that she was getting flowers delivered at our place. The delivery lady at least was provided my number and called me to ask where she could put the flower, she couldn't really leave them outside at -20°C. I was able to quickly unlock the door for her and watch her leave the flowers on the table with the indoor cameras.
8. Adjust the heat pump temperature (eg: in the winter, reduce the temperature considerably during the night)
9. Being able to open & close the blinds by the press of a button. I feel like I'm living in the future 😆. Eventually I'll automate them with the sunrise / sunset.
10. I didn't received my plant's moisture monitor but I'm looking forward to being able to automate a notification to water the plant. It'll be useful too when we're away for an extended amount of time so that I can ask a family member to go water specific plants 😊.
11. Having an alarm for when we leave for more than a few hours (eg: sleeping away). It's insanely loud and have proven itself reliable so far for when I forgot to disarm it (sorry sister 😅!).

### Adaptive Lighting
This is my #1 favorite. I find it amazing to always have the perfect lighting in the house. That's when I actually stop to think about it, because otherwise, I really never think about it. That's how cool it is. I don't have to think to reduce the brightness of a light or feel like a light is too bright, too warm, too cold. It's just almost always perfect. I say almost because I did find myself having to take manual control once in a while but there are such isolated and rare events that they're not even worth mentioning. I highly recommend looking at this integration ([link](https://github.com/basnijholt/adaptive-lighting)).

### Zigbee / zigbee2mqtt
I really like Zigbee as a protocol, it feels solid and stable. I can buy any brand and rely on zigbee2mqtt to have an adapter for it. And if there's none, I can create one and open a PR to have it added, which is actually what I did for the Schlage Smart Deadbolt I bought off Amazon even without any review! I can also buy different coordinator / router if I'm not happy with one I have. Zigbee are not the cheapest but also not the most expensive and are usually good quality. IKEA has a good variety of devices and is a big name. Xiaomi (Aqara etc) also makes amazing Zigbee devices. IMO the choices are much better than WiFi devices. I never tried Z-Wave so I have nothing to say about it.

### Aqara / any Xiaomi devices
They're just well made, reliable and have good community support.

## What I can live with
### localtuya
localtuya is a very good alternative to the official tuya integration. It's reliable and, from my experience, pretty fast.

## What I dislike
I don't like smart 2.4Ghz WiFi devices. They're picky on the signal, often have delays and can easily become unavailable.

### Tuya
I really dislike the Tuya integration, it's a PITA to maintain, it often breaks or disconnects, has often long delays, etc. I tried buying "better" (I thought) bulbs from Costco from a reputable brand, Globe, and I dislike them just as much, if not more since they were a bit more expensive.

## What I look forward to try
- Energy consumption: I'd like to know my consumption by breaker and/or devices.
- Use the weather conditions more.
- Have more of the simple automations (motion detect -> turn on light).
- Use my existing sensors more (currently have no automation based on temperature or humidity).
- Monitor the indoor air quality.
