---
title: My homelab and what's next?
description: This is my homelab; part learning space, part therapy, part “am I still good at this?”
author: kry
date: 2025-05-01 08:40:00 +0100
tags: [LearningInPublic,Homelab]

mermaid: true
image:
  path: /assets/img/headers/kryworks_server.webp
  alt: My full-blown, rockstar homelab! Please ignore the mess behind the devices. It's just part of the "creative chaos". Totally intentional. 👀
---

Back when I started out as a software engineer, I wasn’t working in big corporate teams. It was small setups and you had to do everything: frontend, backend, databases, design, setting up IIS, dealing with servers and networking, even configuring ancient dot-matrix printers for invoicing. Not everything was A++ grade and some parts were a mess but weirdly satisfying. And everything worked... well, at least most of the time.

As the years went on and I moved into more structured and mature teams, things changed. I focused more, specialized more. Infrastructure and operations gradually shifted to other teams even cloud. That’s how scale works and it’s not a bad thing. It lets you go deeper, sharpen your focus and raise quality. But at some point, I missed getting my hands dirty.

I missed that feeling of building something end-to-end. The messy, full-stack kind of work, like when your cron job is running... but nothing’s actually happening. Logs are empty. Is it time zones? Permissions? A silent fail? Who knows. Good luck! So I decided to spin up a homelab, just for myself. Add in some Terraform, Ansible, containers and the joy of breaking things without a heart attack (unless I kill the internet while my wife’s on a work call... lesson learned).

Honestly, I just wanted to see if I’ve still got it.

This setup isn’t fancy or expensive, but it’s real. It teaches me a lot and keeps me sharp. Plus, mixing in some cloud makes it hybrid and closer to real-world environments even if it’s a few steps below production-grade.

## Gear & Devices

I’m keeping things **simple, affordable and wife-approved 💪** at home.

Here’s what I've got;

- **Beelink Mini S12 Pro Mini PC** – My main Proxmox server
- **HSIPC J4125 Quad-Core Firewall Box** – Running bare-metal pfSense
- **Netgear GS305-300PES 5-Port Gigabit Switch** – To connect our media devices
- **Netgear GS308E 8-Port Managed Switch** – Layer 3 managed switch for core traffic
- **Synology NAS** – My one and only NAS; it’s old, but it gets the job done, backing NFS shares in K3s as Persistent Volume and general backups
- **My 2 times upgraded old friend (i7 + 48GB RAM + RTX 4060 Ti)** – My RTX 4060 box. It was my main workstation along with MacBook Pro; now re-purposed for AI stuff (hello, Ollama), but it's currently napping. Its time will come
- **InLine 19" Wall-Mounted Rack + Digitus Patch Panel** – My intention was to make things cleaner, didn't make much but it looks cooler than before. Check the photo above 👆
- **pyur Cable Modem** – Came with the apartment, bundled with painfully slow internet (I miss my fiber back in New Zealand 😢)
- **MacBook Pro 15-inch (2018, 2.6 GHz i7, 16 GB)** – My daily driver. Noisy and hot, but like everything else here, it does the job.

### What I'm Running

Here’s what’s running in the homelab right now:

**pfSense**
: pfSense is my go-to open-source firewall, handling VLANs, DNS, reverse proxy and more. It's all on a single node, so while it's powerful, managing it without a standby replica can sometimes be a challenge, especially during maintenance or updates. I’ve honestly lost count of how many times I’ve heard that sweet, loving voice from the other room: “🤬 Is the internet down again?!”

**Proxmox**
: I use Proxmox as my hypervisor for all my VMs. Right now, I’ve got two nodes, but they're not clustered. One’s dedicated to AI experiments and is currently offline. I’ve automated most of the provisioning with Terraform and Ansible, which makes deployments and environment setups much smoother.

**3-node HA K3s cluster**
: My 3-node K3s setup is running inside Proxmox and I’m using HA embedded etcd for Kubernetes testing. The idea is to eventually migrate it to bare metal, with the goal of managing all my apps through Kubernetes down the road, one day.

Here some application I run; 

- **Omada Controller** - Manages my multi-SSID network via TP-Link access points.
- **Home Assistant** - Centralized integration platform for all smart home devices.
- **Node.js + PostgreSQL + Grafana** – In-house app that aggregates and visualizes health data from our iOS devices, displayed within the Home Assistant dashboard.
- **Traefik** - A reverse proxy for my containerized services. 
- **HAProxy** - External load balancer for K3s and reverse proxy for various services. 
- **Apache Guacamole** - Gives me remote access to my Windows 11 VM on Proxmox. But I am not using Windows this days much.
- **CommaFeed** - My preferred self-hosted RSS reader and currently the only app running on my K3s cluster.
- **Self-hosted GitHub Runner** - For building and deploying projects in my CI/CD pipeline.
- **KryWorks Blog (*staging*)** - A preview environment for blog posts before they go live.

Beside of these, I also utilize some basic **AWS Services** such as S3, CloudFront, Route 53 for my static site and CI/CD along with **Cloudflare**.

## Next Up

If you’ve read [my last post](/posts/rejections-realizations-a-new-chapter), you already know the backstory. This isn’t a startup, or a side hustle, or a shiny YouTube channel with RGB lights (_though I do love LEDs 😎 and if I ever launch one, just pretend this post doesn’t exist_). It’s just a place to build in public. A way to stay hands-on, explore new tools and stay connected to the field.

Honestly, I jumped into this by bouncing between networking, containers, software development, cloud, AI, security and DevOps. It works... but it’s far from clean.

So next, I'd like to clean up the mess and revisit some of the parts of the setup with fresh eyes. In the middle I also would like to share some coding projects, some dev tools like DevContainers that I am currently using with this Jekyll app and further more small field notes; little wins, fails, or takeaways from side gigs and volunteer work.

Until then: stay curious, keep shipping.
   
Cheers,   
**— Koray**
