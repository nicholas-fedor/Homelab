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

### Networking

#### Initial/Basic Setup

The project initially started with both the Proxmox host, Docker VM, and
containers all sharing the same VLAN (VLAN 50).

Each Proxmox Host has the following addressing scheme:

```text
PVE1: 192.168.50.51
PVE2: 192.168.50.52
PVE3: 192.168.50.53
```

The Docker VM resides within the cluster with an IPV4 address of
`192.168.50.224`.

Docker containers running within the Docker VM share the `192.168.50.224`
address; however, Traefik is used to route requests based on a particular URL to
a service at a specified port.

##### An Improvement

Instead of the Docker VM sharing the Proxmox host network, it's preferable to
place the VM on its own network by setting a VLAN tag within the Proxmox settings.

#### Macvlan Setup

[Docker Tutorial](https://docs.docker.com/engine/network/tutorials/macvlan/)

Docker has some interesting functionality regarding networking.  
Instead of containers relying upon the host IP address, it's possible for
containers to be assigned IP addresses within their own VLAN.

As an example, if we create a separate VLAN 40 on our home network, then create
a corresponding Macvlan 40 network using Docker, we will be able to have
containers with each their own IP address assigned based on the range permitted
by the corresponding VLAN 40 subnet.

This can be best accomplished via the CLI on the Docker host:

1. Determine the host's network adapter name (ex. enp6s18):

   ```console
    ip link
   ```

2. Create the Docker network using the Macvlan driver:

  ```console
  docker network create \
  -d macvlan \
  -o parent=enp6s18.40 \
  --subnet=192.168.40.0/24 \
  --gateway=192.168.40.1 \
  --ip-range=192.168.40.128/25 \
  macvlan40
  ```

  This will create a Macvlan network using the respective network settings,
  including establishing the DHCP range between 192.168.40.128 to
  192.168.40.254.
  An important note, including the `.40` tag on `enp6s18` will create the
  interface on the host as a 802.1Q trunked bridge, therefore allowing network
  communication from containers attached to the `macvlan40` network to both the
  Docker host and other VLANs on the network.

  Note, setting a higher DHCP range also allows flexibility in the future for
  statically assigning IP addresses to containers in the lower range of the
  subnet, i.e. 192.168.40.10. This is particularly helpful if using containers
  for network-related services, such as DNS servers.

  > I tested using Portainer to setup Macvlan networking and found it was not
  > suitable for this particular operation. This may be a permissions
  > configuration issue on my end; however, it resulted in headaches until
  > manually configuring via the Docker host CLI.

## Administration Setup

### VSCode

Initially accessed and managed VM via Windows Terminal; however, I've shifted
over to using VSCode, which has enabled easier file editing and management.
It also has several extensions that make life easier.

For initial Git-related handling, I have used GitHub Desktop; however, I will
likely fully setup Git on the VM, including adding GPG and SSH keys to GitHub.

----------

[Return to top](/SETUP.md)

----------
