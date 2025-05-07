---
title: A Smarter Way to Set Up Development Environments with Dev Containers
description: Provisioning developer environments is more than just setting up your machine. It’s about ensuring your team can work effectively, regardless of their individual setup. In this post, I’ll discuss how Dev Containers can streamline environment setup and address common scaling issues that affect both individual developers and teams.
author: kry
date: 2025-05-07 09:15:00 +0100
tags: [LearningInPublic,SoftwareEngineering,DeveloperExperience,Dev Containers,EnvironmentSetup,Docker]
pin: false
image:
  path: /assets/img/headers/kryworks_containers.webp
  alt: I might just stick with the same image for all my container-related articles. It just fits!
---

## Manual Setups, Inconsistent Environments

Over the years, both as a developer and engineering leader, I’ve seen how inconsistent setups drain focus, morale and time. Whether onboarding a new hire or getting a team member from another group to contribute, setting up development environments can be one of the most overlooked pain points.

Some companies provide developer machines with pre-built OS images that include selected software, while others expect developers to install the necessary tools themselves. Some companies also use automation tools like Ansible playbooks to handle the installation of required development tools. The goal of this process is to equip developers with the right tools to set up their projects on the machine, rather than to begin working on them immediately.

The distinction between provisioning a dev machine (getting the right tools on your system) and setting up a project (handling dependencies) is essential.

> “Oh yeah, you need Node 18, but also Ruby 2.7 for the static site. Don’t forget to tweak this config manually. Here is the Confluence link where you can read the procedure. Good luck 🍀”
> 
> _Does that resonate with you?_

### Time Consuming Manual Steps

Developers spend a significant amount of time installing dependencies, configuring environments and troubleshooting mismatched versions. Setting up the projects on the new machines often involves more **manual steps** than it should.

### Inconsistent environments

Tools and libraries clashing at the OS level create a **fragile and inconsistent environments** that’s hard to reproduce or scale. While developers can use framework-specific tools like NVM to isolate Node.js versions to prevent any conflicts, they may not have the same flexibility for the language frameworks required for their assigned projects.

## Dev Containers

**[Dev Containers](https://containers.dev/)** solves these issues by isolating project dependencies from the host environment.

For those unfamiliar, 

> A **development container (or dev container for short)** allows you to use a container as a full-featured development environment. It can be used to run an application, to separate tools, libraries, or runtimes needed for working with a codebase and to aid in continuous integration and testing. Dev containers can be run locally or remotely, in a private or public cloud, in a variety of supporting tools and editors.

A Dev Container handles the environment setup **within the container**, ensuring everything runs in isolation without any host pollution (this is important for my old pal Mac 💻), including dependencies, VS Code extensions, your favourite shell, etc.

![Desktop View](/assets/img/architecture_dev_containers.png)
_Developing inside a Container. Image via [Visual Studio Code](https://code.visualstudio.com/docs/devcontainers/containers)_

By using containers, you get:

1. **Consistency**: No more "Which NodeJS version do I need?" moments. Plus, consistent linting settings, extensions across teams and many other benefits provided by the dev container configuration.
2. **Portability**: Share a complete, reproducible environment across the team and machines way faster than manual setups.
3. **Zero pollution**: Run projects in isolated containers without messing with your system setup.

To start working with Dev Containers, you need 

1. [VS Code](https://code.visualstudio.com/download)
2. [VS Code Dev Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
3. [Docker](https://www.docker.com/get-started/)

Please note that you can also use [Dev Container CLI](https://code.visualstudio.com/docs/devcontainers/devcontainer-cli) if you use another editor or terminal.
 
### Dev Containers in Action: KryWorks Blog

I’ve been using Dev Containers for KryWorks Jekyll blog, the one that you are reading 🤓. 

**Without** a Dev Container, getting Jekyll to run locally means;

1. Install Ruby (**2.7.0** or higher)
2. Install RubyGems
3. Install GCC
4. Install Make
5. Install jekyll and bundler gems
6. Clone the repo you'll be working on (or create a new site: `jekyll new myblog`)
7. Open the editor, apply your changes
8. Run the site locally: `bundle exec jekyll serve`

**With** a Dev Container, you can skip installation part you can jump straight to

1. Clone the repository. For example, the [Jekyll Chirpy Theme](https://github.com/cotes2020/jekyll-theme-chirpy), which I’m using and supports Dev Containers.
2. Open the project in VS Code and run it in a container. Press `Cmd+Shift+P` (or `Ctrl+Shift+P` on Windows) and Select `Dev Containers: Reopen in Container`.
3. Run the site locally with the command: `bundle exec jekyll s --livereload`

Pretty cool, isn't it? For a simple static site, this can feel easy, but imagine scaling this to a larger app with multiple dependencies and configuration steps and orders.

## The Caveats

Dev Containers are not a one-size-fits-all solution. Here are a few things to consider:

1. **Performance**: Containers can be slower than running natively on your system, especially for resource-heavy apps. Thankfully, I don't have a resource-heavy app in my own repositories at this point.
2. **Complexity in Scaling**: For larger projects or microservices, maintaining containers across teams can get complicated. I am working on this currently and hopefully, I will write an article about it in the future.
3. **Learning Curve**: Developers must understand container management and how to configure Dockerfiles and `devcontainer.json` files. But that would be a great investment for your team, your company and most importantly for the individuals at your team for their future career.
 
## Dev Containers at the Team Level

For teams, Dev Containers can drastically improve consistency across different dev environments. But scaling them across larger projects requires careful planning.

The key is **neither to overcomplicate nor oversimplify it.** 

1. **Educate yourself and team**. Learn the concept well and understand the limitations of Dev Containers.
2. **Plan effectively**. Use data to measure improvements and have discussions within the team.
3. **Consider automation and deployment pipelines**. Ensure they align with the use of Dev Containers.
4. **Start small, learn quick, iterate often**. Begin with a pilot project using Dev Containers and expand as you see the benefits.

## Final Thoughts

While this article focuses on the specifics of Dev Containers, rather than the broader concept of Developer Experience (DX), it’s important to note that treating DX as a cultural priority rather than just a set of tools and processes can lead to better collaboration, faster onboarding and ultimately, more impactful engineering outcomes.

Dev Containers are just one tool in a larger strategy that includes automation, culture and communication. Adopting them can enable developers to spin up environments quickly, collaborate seamlessly and focus on solving problems rather than troubleshooting setups.

Personally, I’ve found them incredibly useful for my blog and I’ve already started converting other projects and recommending them to my clients when appropriate.

Start small, experiment and you’ll see the benefits firsthand. I promise, your future self (and your teammates) will thank you.

Cheers,  
Koray
