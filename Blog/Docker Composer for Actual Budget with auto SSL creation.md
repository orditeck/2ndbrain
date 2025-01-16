---
title: Docker Composer for Actual Budget, with auto SSL creation
created: 2025-01-15
modified: 2025-01-15
---
The other night, I only had a few precious minutes free to myself. And how better to use that time but to quickly set up an [Actual Budget](https://actualbudget.org/) server!

I use Portainer to manage my Docker containers, through _Stacks_. They're basically `docker-compose.yml` files. 

Since AB (that's Actual Budget) is running is on a server in my house and not directly on the computer from which I want to access it, I cannot use `localhost:5006`. It's not running locally. I have to use `10.1.0.42:5006` . However, I was welcomed by this:

> _Actual_ requires access to _SharedArrayBuffer_ in order to function properly

K. Quick Google. SharedArrayBuffer needs https. K. _Try https_. Doesn't work. It doesn't have a certificate. Great.

So this, below, is the simple `docker-composer.yml` I wish I had found during that short free time that flew away like summer. I would've enjoyed it more. Here ya go stranger, enjoy the sun!

```
version: '3.1'
services:
  generate_ssl:
    image: alpine
    volumes:
      # Gotta be the same as below
      - ./actual-data:/data
    entrypoint: ["/bin/sh","-c"]
    command:
    - |
      apk add openssl
      openssl req -x509 -nodes -days 365 -subj  "/C=CA/ST=QC/O=Company/CN=website.com" -newkey rsa:2048 -keyout /data/selfhost.key -out /data/selfhost.crt
  actual_server:
    image: docker.io/actualbudget/actual-server:latest
    ports:
      - '5006:5006'
    environment:
      - ACTUAL_HTTPS_KEY=/data/selfhost.key
      - ACTUAL_HTTPS_CERT=/data/selfhost.crt
    volumes:
      - ./actual-data:/data
    restart: unless-stopped
```

---
Oh, by the way, if you have a better way to do this, please share below, for the greater good!