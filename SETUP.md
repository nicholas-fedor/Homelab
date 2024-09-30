# Nick's Homelab - Setup Documentation

**[Return to Home](/README.md)**

## Foreword

This is intended to document the setup of the host virtual machine that's
running Docker and the subsequent applications.

## Host Machine Setup

Currently using an Ubuntu virtual machine with a Proxmox 3x mini-pc cluster.
This is intended to be a simple solution; however, I am interested in exploring
options for using Talos Linux to run a unified K8S cluster across all three
nodes.

## Virtual Machine Setup

The Ubuntu 24.04 VM is a linked clone from a template that I created.
This means that changes to the template will impact this VM.

The VM's template is setup to use both my locally-hosted DNS and NTP servers, in
addition to using DoT for DNS resolution.

### Storage

Storage is currently setup via a NFS Share entry in `/etc/fstab`, mounted to `/mnt/Truenas/Apps`, and
symlinked to `/home/nick/Apps`.

The symlink is intended to prevent FS issues with the home directory if the
Truenas NFS share is disrupted.

The Truenas NFS configuration is set to translate FS operations from the VM as
root. This is not ideal and will need to be adjusted later.

## Docker Setup

## Administration Setup

### VSCode Setup

Initially accessed and managed VM via Windows Terminal; however, I've shifted
over to using VSCode, which has enabled easier file editing and management.
It also has several extensions that make life easier.

For initial Git-related handling, I have used GitHub Desktop; however, I will
likely fully setup Git on the VM, including adding GPG and SSH keys to GitHub.

----------

[Return to top](/SETUP.md)

----------
