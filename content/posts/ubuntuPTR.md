---
title: Use PTR record to set Ubuntu Hostname on autoinstall
date: 2021-06-26
description: How to set the hostname for an Ubuntu autoinstall using the PTR record of the server's IP.
draft: false
authors:
  - couchllama

tags:
  - ubuntu

geekblogToC: 3

geekblogAnchor: true
---

I've been working on redoing my homelab setup. I’m moving from running a
cluster of bare metal Ubuntu NUCs to running Ubuntu VMs on top of proxmox. Part
of this setup is using my old pxeboot setup that installs Ubuntu that way. One
of the issues I ran across was getting the hostname to be set from DNS. It
turns out that in order for this to work correctly you need to edit the
hostname variable in /autoinstall.yaml using early-commands. I’m doing this by
using nslookup to pull my hostname from a PTR record and use it to update the
autoinstall.yaml with sed:

    sed -i "s+ubuntu-server+$(nslookup $(hostname -I | awk '{print $1}') | awk -F'[ .]' 'NR==1{print $8}')+" /autoinstall.yaml

My full autoinstall yml looks like:

    #cloud-config
    autoinstall:
        version: 1
        identity:
          hostname: ubuntu-server
          username: ansible
          password: [HASH]
        storage:
          layout:
            name: direct
        packages:
          - qemu-guest-agent
        update: yes
        ssh:
          install-server: true
          authorized-keys:
            - ssh-ed25519 [PUBLIC KEY]
        early-commands:
          - sed -i "s+ubuntu-server+$(nslookup $(hostname -I | awk '{print $1}') | awk -F'[ .]' 'NR==1{print $8}')+" /autoinstall.yaml
        late-commands:
          - curtin in-target --target=/target -- systemctl enable qemu-guest-agent
          - curtin in-target --target=/target -- apt update
          - curtin in-target --target=/target -- apt upgrade -y
