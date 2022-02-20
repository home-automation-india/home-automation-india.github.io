---
parent: HomeAssistant
title: External Access through Oracle and Tailscale
---

# Accessing Internal Apps through Oracle, Cloudflare and Tailscale with Your Domain

This doc describes how you can access your home network from outside, with the help of Oracle cloud instance, Tailscale, Nginx Proxy Manager and Cloudflare. This doc expects you to have a Domain name, which will be used for connecting from the internet. 

## Why Do You Need it?

We always find in situations where we need to access locally hosted services online. More often than note, most of us are behind a double-nat, making it impossible to do so without opting for static IP from the ISP, which introduces us to a whole new lot of problems. This set-up, can help you run a tunnel from your local instance to an online instance, making it possible to access these services from the internet. 


## What Do You Need?

- A domain name - duh!
- An Oracle Always Free instance - Ampere
- Cloudflare
- Tailscale
- Docker
- Nginx Proxy Manager on Docker
- Maria DB on Docker
- Putty and Puttygen or Terminal

## Oracle Always Free Instance

Oracle offers always free services. 

- Click this link: https://www.oracle.com/in/cloud/free/
- Create an account, by clicking on Start for Free
- Sign-up, and verify your account. 

### Creating a New Instance

Click on the menu on the left-hand side top, and choose **Instances** under **Compute**

![Create a New Oracle Instance]: 



