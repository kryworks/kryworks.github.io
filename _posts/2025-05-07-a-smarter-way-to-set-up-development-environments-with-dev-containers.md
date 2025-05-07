---
title: A Smarter Way to Set Up Development Environments with Dev Containers
description: Provisioning developer environments is more than just setting up your machine. It’s about ensuring your team can work effectively, regardless of their individual setup. In this post, I’ll explain how Dev Containers can streamline environment setup and address common scaling issue and improve onboarding across teams.
author: kry
date: 2025-05-07 09:15:00 +0100
tags: [LearningInPublic,SoftwareEngineering,DeveloperExperience,Dev Containers,EnvironmentSetup,Docker]
pin: false
image:
  path: /assets/img/headers/kryworks_containers.webp
  alt: I might just stick with the same image for all my container-related articles. It just fits!
---

## The Problem with Manual Setups

Over the years, both as a developer and engineering leader, I’ve seen how inconsistent setups drain focus, morale and time. Whether onboarding a new hire or getting a team member from another team to contribute, setting up development environments can be one of the most overlooked pain points.

- Version mismatches (e.g., “Which NodeJS version do I need?”)
- Missing or misconfigured dependencies
- Conflicting tools at the OS level (e.g., NVM to isolate Node.js versions)
- Outdated or unclear documentation

Companies might ship pre-built OS dev images or use tools like Ansible to help developers to set up their environments faster. However, these solutions are meant to provision a base machine, but not to handle per-project dependencies. That’s where Dev Containers shine.

## Dev Containers

**[Dev Containers](https://containers.dev/)** allows you to define a complete development environment, OS, tools, runtimes, extensions inside a container that can be run locally or remotely. With VS Code and Docker, developers can spin up standardised, reproducible environments without polluting their host system.

![Desktop View](/assets/img/architecture_dev_containers.png)
_Developing inside a Container. Image via [Visual Studio Code](https://code.visualstudio.com/docs/devcontainers/containers)_

By using containers, you get:

1. **Consistency**: Everyone uses the same versions and tools. Plus, consistent linting settings, extensions across teams and many other benefits provided by the dev container configuration.
2. **Portability**:  Clone and go, across devices and teams.
3. **Zero pollution/Isolation**: Avoid host conflicts and OS-specific issues. Run projects in isolated containers without messing with your system setup.

While this article focuses on local development using VS Code and Docker, it's worth noting that Dev Containers also power [GitHub Codespaces](https://docs.github.com/en/codespaces), a cloud-hosted version of your dev setup. It's great for remote work, quick contributions, or using low-powered machines.

To start working with Dev Containers, you need 

1. [VS Code](https://code.visualstudio.com/download)
2. [VS Code Dev Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
3. [Docker](https://www.docker.com/get-started/)

Please note that you can also use [Dev Container CLI](https://code.visualstudio.com/docs/devcontainers/devcontainer-cli) if you use another editor or terminal.
 
### Dev Containers in Action: KryWorks Blog

I’ve been using Dev Containers for KryWorks Jekyll blog, the one that you are reading. 

**Without** a Dev Container, getting Jekyll to run locally means;

1. Install Ruby (**2.7.0** or higher)
2. Install RubyGems
3. Install GCC
4. Install Make
5. Install jekyll and bundler gems
6. Clone the repo you'll be working on (or create a new site: `jekyll new myblog`)
7. Open the editor, apply your changes
8. Run the site locally: `bundle exec jekyll serve`

**With** a Dev Container, you can skip the installation step and you can jump straight to cloning.

1. Clone the repository. For example, the [Jekyll Chirpy Theme](https://github.com/cotes2020/jekyll-theme-chirpy), which I’m using and supports Dev Containers.
2. Open the project in VS Code and run it in a container. Press `Cmd+Shift+P` (or `Ctrl+Shift+P` on Windows) and Select `Dev Containers: Reopen in Container`.
3. Run the site locally with the command: `bundle exec jekyll s --livereload`

> Pro Tip: Use postCreateCommand in your devcontainer.json to automate setup tasks like installing language-specific dependencies (e.g., `npm install`) so environments are fully ready without extra manual steps.
{: .prompt-tip }

That’s it! No local Ruby or gem setup is needed. This can feel easy for a simple static site, but imagine scaling this to a larger app with multiple dependencies and configuration steps and orders.

## The Caveats

Dev Containers are not a one-size-fits-all solution. Here are a few things to consider:

1. **Performance**: Can be slower than native execution for heavy apps. Especially on MacOS, file system mounts via Docker can be slow, especially for large projects.
2. **Complexity**: Managing multiple containers across microservices requires orchestration (consider Docker Compose).
3. **Learning Curve**: Teams need to understand Dockerfiles, volume behaviour and container configs. Learning these concepts is a valuable long-term investment for your team, your company and most importantly for the individuals at your team for their future career.
 
## Dev Containers at the Team Level

For teams, Dev Containers promote environment consistency, smoother onboarding and fewer “it works on my machine” moments. But scaling them across larger projects requires careful planning.

The key is **neither to overcomplicate nor oversimplify it.** 

1. **Educate yourself and team**. Learn the concept well and understand the limitations of Dev Containers.
2. **Start small, learn quick, iterate often**. Pilot before scaling. You can try it on a sandbox or internal tool project.
3. **Consider automation and deployment pipelines**. Integrate container usage into CI/CD and infrastructure-as-code where possible.
4. **Measure impact**. You can track onboarding time and support tickets pre and post-adoption.

## Final Thoughts

Dev Containers are one part of a bigger developer experience (DX) strategy. When used thoughtfully, they reduce friction, speed up onboarding and let engineers focus on solving problems rather than troubleshooting setups.

I’ve found them incredibly useful not only for my personal projects but also in consulting. I now recommend them to clients whenever context allows.

Start small, iterate and scale. Your future team will thank you.

Cheers,  
Koray
