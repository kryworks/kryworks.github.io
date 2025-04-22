---
title: My homelab and what's next?
description: This is my homelab; part learning space, part therapy, part “am I still good at this?”
author: kry
date: 2025-04-22 10:01:00 +0100
tags: [LearningInPublic,Homelab]

mermaid: true
image:
  path: /assets/img/headers/kryworks_server.webp
  alt: My full-blown, rockstar homelab! Please ignore the mess behind the devices. It's just part of the "creative chaos". Totally intentional. 👀
---

## Why am I doing this?

First of all — because I can. I love messing with electronics and occasionally breaking things. But that’s not the main motivation here.

If you’ve read [my last post](/posts/rejections-realizations-a-new-chapter), you already know the broader story. What I am trying to do here is not a product, a startup, or a shiny YouTube channel with RGB lights (*though I do love LEDs 😎 and if I ever launch one, just pretend this post doesn’t exist*).

I just wanted to create my personal space to build in public. It’s also a way to stay sharp, relevant, and connected with the industry.

## Gear & Devices

I’m keeping things **simple, affordable, and wife-approved 💪** at home.

Here’s what I've got;

- **Beelink Mini S12 Pro Mini PC** – My main Proxmox server
- **HSIPC J4125 Quad-Core Firewall Box** – Running bare-metal pfSense
- **Netgear GS305-300PES 5-Port Gigabit Switch** – To connect our media devices
- **Netgear GS308E 8-Port Managed Switch** – Layer 3 managed switch for core traffic
- **Synology NAS** – My one and only NAS; it’s old, but it gets the job done, backing NFS shares in K3s as Persistent Volume and general backups
- **My 2 times upgraded old friend (i7 + 48GB RAM + RTX 4060 Ti)** – My RTX 4060 box. It was my main workstation along with MacBook Pro; now re-purposed for AI stuff (hello, Ollama), but it's currently napping. Its time will come
- **InLine 19" Wall-Mounted Rack + Digitus Patch Panel** – My intention was to make things cleaner, didn't make much but it looks cooler than before 😊 
- **pyur Cable Modem** – Came with the apartment, bundled with painfully slow internet (I miss my fiber back in New Zealand 😢)
- **MacBook Pro 15-inch (2018, 2.6 GHz i7, 16 GB)** – My daily driver. Noisy and hot, but like everything else here, it does the job.

### What I'm Running

Here’s what’s running in the homelab right now:

**pfSense**
: pfSense is my go-to open-source firewall, handling VLANs, DNS, reverse proxy, and more. It's all on a single node, so while it's powerful, managing it without HA can sometimes be a challenge, especially during maintenance or updates. I’ve honestly lost count of how many times I’ve heard that sweet, loving voice from the other room: “🤬 Is the internet down again?!”

**Proxmox**
: I use Proxmox as my hypervisor for all my VMs. Right now, I’ve got two nodes, but they're not clustered. One’s dedicated to AI experiments and is currently offline. I’ve automated most of the provisioning with Terraform and Ansible, which makes deployments and environment setups much smoother.

**3-node HA K3s cluster**
: My 3-node K3s setup is running inside Proxmox, and I’m using HA embedded etcd for Kubernetes testing. The idea is to eventually migrate it to bare metal, with the goal of managing all my apps through Kubernetes down the road, one day 😊.

Here some application I run; 

- **Omada Controller** - Manages my multi-SSID network via TP-Link access points.
- **Home Assistant** - Centralized integration platform for all smart home devices.
- **Node.js Web API + PostgreSQL + Grafana** - Aggregates and visualizes health data from our iOS devices, displayed within the Home Assistant dashboard.
- **Traefik** - A reverse proxy for my containerized services. 
- **HAProxy** - External load balancer for K3s and reverse proxy for various services. 
- **Apache Guacamole** - Gives me remote access to my Windows 11 VM on Proxmox. But I am not using Windows this days much.
- **CommaFeed** - My preferred self-hosted RSS reader, and currently the only app running on my K3s cluster.
- **Self-hosted GitHub Runner** - For building and deploying projects in my CI/CD pipeline.
- **KryWorks Blog (*staging*)** - A preview environment for blog posts before they go live.

Beside of these, I also utilize some basic **AWS Services** such as S3, CloudFront, Route 53 for my static site and CI/CD along with **Cloudflare**.

## Next Up

I’ll be honest. I jumped into this by bouncing between networking, containers, software development, cloud, AI, security, and DevOps. It works… but it’s far from clean.

Next, I’ll be revisiting each part of the setup with fresh eyes. Refining, simplifying, and sharing what I learn along the way. No roadmap, just following my curiosity and building in public or more of refactoring in public. 

In between, I’ll also share quick “field notes”, little wins, fails or learnings from the volunteer projects and side gigs I’ve been helping with.

That’s the plan for now but like any good project, it’ll evolve.

Until then: stay curious, keep shipping.  
   
Cheers,   
**— Koray**
