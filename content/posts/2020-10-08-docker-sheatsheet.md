---
template: SinglePost
title: Docker and it's Terminology
status: Published
date: 2019-09-07
featuredImage: https://ucarecdn.com/e9d5d846-c6ab-4855-8fbb-2b8e7a1dc411/
excerpt: Definitions and Cheatsheet for Docker App
categories:
  - category: Tech
meta:
  title: ""
  description: In this post I will explain each terms used when using or dealing
    with Docker along with Docker's cheatsheet, this will act as a guide to
    anyone who is interested to learn more about *containerization.*
---
**Docker** has revolutionized the way how developers ship, build and run today's application. Docker provides the ability to package and run an application in a loosely isolated environment called a *container*. It solves the main problem of *"It works on my machine"* that a team of developers have when dealing with different versions of back-end software installed on their different machines.

![Containers vs. VM](https://ucarecdn.com/907b261b-4bde-45a4-ac0b-eec4293fc851/ "Containers vs. VM")

In this post I will explain each terms used when using or dealing with Docker, this will act as a guide to anyone who is interested to learn more about *containerization.*

**Containerization:** term used that involves bundling an application together with all of its related configuration files, libraries and dependencies required for it to run in an efficient and bug-free way across different computing environments. The most popular containerization ecosystems right now are Docker ,Kubernetes and AWS ECS.

**Docker Image:** A static snapshot of container's configuration. This manages your Container .config.

**Docker Container:** an application sandbox. basically your running app that runs in an isolated environment. cannot interact with your computer(Host) directory unless you specify it to.

**Layers**: Docker image is composed of read-only file system layers, while container creates single writable layer.

**Docker Registry**: Remote server for storing Docker images. Repository for docker images in a way. Hosted on hub.docker.com.

**Docker Client**: Client app that interact with local or remote Docker Daemon.

**Docker Daemon**: service process that listens on port to Docker client commands, whether it's locally or remotely.

**Docker Host**: This will be the server/computer that runs the Docker engine..

**Docker Volume**: directory folder that is shared between the host and the running container.

Now you can see why a team of developers / IT professionals much prefer using Docker when developing an app. Not only it enables stable development across different machines, it's also a powerful tool when combined with Jenkins. Below is a preview on Continuous integration (*CI*) and continuous delivery (*CD*) using Docker and Jenkins that runs on Cloud server.

![CI/CD with Docker and Jenkins](https://ucarecdn.com/e3b0991c-96b5-4423-b168-6229bf7bd5d4/ "CI/CD with Docker and Jenkins")

If you haven't try Docker don't be shy to use it on your own Node.js Project! on my next blog I will post the cheatsheet on how to use Docker.