---
title: Developer Experience (DX) Is Culture, Not Just Tooling
description: Provisioning your workstation is not the same as preparing your project. In this article, I share how DevContainers help bridge that gap with cleaner, portable environments.
author: kry
date: 2025-05-06 09:15:00 +0100
tags: [LearningInPublic,SoftwareEngineering,DeveloperExperience,DevContainers,EnvironmentSetup,Docker]
pin: false
image:
  path: /assets/img/headers/kryworks_containers.webp
  alt: I might just stick with the same image for all my container related articles. It just fits!
---

Over the years, both as a developer and later as an engineering lead, I’ve seen how the smallest technical problem can drain focus, morale, and time (and money) from engineering teams.

Setting up development environments is one of the most common pain points.

Whether it’s a new hire trying to get a project running or a developer from another team helping out, we often underestimate how fragile and inconsistent dev setups really are.

## Old friend: README files

I’ve joined teams where the onboarding guide was a README (or Confluence page, SharePoint document, etc., you get the point) with a list of dependencies longer than the actual source code. And the tribal knowledge goes like:

> “Oh yeah, you need Node 18, but also Ruby 2.7 for the static site. Don’t forget to tweak this config manually, here is the README.md you can follow. Good luck 🍀”

These setups don’t scale. Not across teams, not across machines, and not across time.

## Provisioning is not the same as setting up a project

The scenario is similar in my own dev setup. Different projects, different prerequisites:

- My Jekyll site uses Ruby
- My health platform runs on Node.js, Postgres, and Grafana
- Some side projects are in .NET Core

It’s a shame, but yes, I also have README files for how to install some projects locally 😅

Before switching back to macOS recently, I started automating my software provisioning and managing my dev machine with Ansible playbooks (still working on one for macOS). They’ve been great for setting up base tools: Docker, VS Code, system packages, shell configs, and even my email client, wallpaper, etc.

With that setup, I could spin up a full dev workstation in under 10 minutes (after the OS install, of course). Very similar to how company laptops work: open your laptop and get coding. But... can you, really?

Provisioning the OS along with the required toolset is not the same as project setup. Software provisioning doesn’t solve project-level isolation. I still had to manually install dependencies per project and might even remove them later to avoid version conflicts.

Sure, I could extend the Ansible playbook. But that would mean: 

- Adding project-specific dependencies to a global setup
- Creating clutter just for the sake of running a project I may touch once
- Highly likely dealing with versioning conflicts


It sounds like creating more problems than just setting up everything manually. But it would still cause a lot of pollution for my old pal Mac—and not to mention, wasted resources.

I needed something self-contained, predictable, and portable.

That’s when I turned to **DevContainers**.

## DevContainers: A Layer Above the OS & Your Core Toolsets

For the unfamiliar, a **DevContainer** defines your development environment as code using Docker. It packages everything your project needs; language runtimes, tools, environment variables, and configs. Fully isolated from your host.

Basically, a DevContainer is a ready-to-go, isolated setup for your project that runs in Docker, so everything just works no matter what machine you're on.

- No more guessing which Ruby or Node version to install
- No global install conflicts
- No tweaking your host just to test something
- No pollution

Just clone the repo, open it, and the container handles the rest.

## Case Study: My Jekyll Blog

Take a standard Jekyll blog. It’s built with Ruby and has some dependencies:

- Ruby **2.7.0** or higher
- RubyGems
- GCC and Make (plus a bit of luck nothing on your system conflicts)

Now, I’m using the Chirpy Jekyll theme, which already ships with a DevContainer.

I just forked it to my GitHub org, cloned it locally, ran it in a DevContainer, and executed it. I didn’t install any of the prerequisites.

At its core, the [Chirpy Jekyll theme](https://github.com/cotes2020/jekyll-theme-chirpy) repo uses the [Jekyll DevContainer base image](https://github.com/devcontainers/images/tree/main/src/jekyll). If you check out the [Dockerfile](https://github.com/devcontainers/images/blob/main/src/jekyll/.devcontainer/Dockerfile), you’ll see how it installs Ruby and required packages.

In addition to the Dockerfile, [devcontainer.json](https://github.com/kryworks/kryworks.github.io/blob/main/.devcontainer/devcontainer.json) installs VS Code extensions and sets up ZSH as the shell as well. Pretty cool isn't it?

## Want to Try It?

You can try this yourself.

1. Install [VS Code](https://code.visualstudio.com/download), [Docker](https://www.docker.com/get-started/), and [Git](https://git-scm.com/downloads) if you haven't yet (I am sure you have 🙂)
    
2. Clone the [Chirpy Jekyll theme](https://github.com/cotes2020/jekyll-theme-chirpy)
    
3. Open it in **VS Code**
    
4. Make sure you’ve installed the **Dev Containers extension**
    
5. Click the bottom-left colorful `><` icon then click **“Reopen in Container”** from the list that pops up
    
6. Wait for everything to install, then run `bundle exec jekyll s --livereload` from the VS Code terminal.
    
7. Visit `http://127.0.0.1:4000/`
    

Boom! Your blog is running locally with no host pollution. Since we use the `--livereload` flag, you can make changes while the app is running and see the updates directly on the browser.

## Or Try a Clean Node.js DevContainer

While the Jekyll example uses an existing DevContainer base image, creating your own DevContainer with a custom Dockerfile helps you understand how all the pieces fit together.

To help with that, I created a minimal Node.js Express API project with a bare-bones DevContainer setup that you can try locally.

🔗 **GitHub Repo:** [kryworks/devcontainer-node-express](https://github.com/kryworks/devcontainer-node-express)

Give it a try, clone it, break it, rebuild it.

For more samples, you can also check out [DevContainer Templates repo](https://github.com/devcontainers/templates)

## Consistency and Confidence

As an engineer, I want to focus on what I’ve committed to, what my actual goal is, such as creating my blog and not spending time to resolve some library version conflict just to run the app locally.

It should be the same for organizations. Every new joiner should feel confident, productive, and unblocked from day one.

You don’t need full-blown platform engineering to improve DX. Sometimes it’s just about reducing the steps between `git clone` and `npm start`.

DevContainers don’t replace CI/CD or infrastructure but they do offer a reliable, versioned, and team friendly way to spin up dev environments that are:

- Reproducible
- Clean
- Portable

## Final Thought

I will start moving more of my projects and even tools like `kubectl`, `terraform` and `ansible` into DevContainers. Well, that’s the plan, but I’m still deciding whether to have a global DevContainer image for core tools or isolate them in individual repos. We’ll see.

I’m also aware that containerized dev environments aren’t a perfect fit for everyone or every setup, but I’d recommend trying it if your projects involve onboarding friction or jumping between stacks.

You don’t need to overcommit. You can start small. But I’m sure your future self and your teammates will thank you.

Cheers,   
**— Koray**
