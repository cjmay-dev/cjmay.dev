# cjmay.dev

Welcome to my homelab! This site serves as a showcase of my homelab as well as my documentation for disaster recovery. I had quite a bit set up already when I decided to open source everything, so this site will initially be a work in progress as I bring everything up to date.

My goals for my homelab:

* security
* automation
* documentation
* stability

You'll notice privacy is not one of my goals. By making a showcase for my homelab and open sourcing most of the code, I'm inherently revealing some information about what I run, and I'm okay with that. I also rely on some cloud providers for "outside my network" stuff like git hosting, VPN, backups, and TLS proxies. Being fully self-contained is not a goal of mine either.

With that intro out of the way, let's check out my homelab!

## Network Diagram

TODO

## Hardware

TODO

## Foundational Infrastructure

My Docker Compose project template relies on the infrastructure below. These systems are laid out in the general order they need to be set up in.

Use the links to navigate to the setup docs for each item.

### Cloud Platforms

* [GitHub](./docs/github/setup)
  * source code management
  * bootstrap secrets
* [Discord](./docs/discord/setup)
  * channel(s) for homelab alert webhooks
* [Tailscale](./docs/tailscale/setup)
  * ci to infrastructure SSH access
* [AWS](./docs/aws/setup)
  * tfstate storage bucket
  * uptime kuma server
* [Backblaze](./docs/backblaze/setup)
  * application key for terraform
* [Cloudflare](./docs/cloudflare/setup)
  * DNS
  * WAF
  * application key for terraform
* [Infisical](./docs/infisical/cloud/setup) (if not self-hosting)
  * common secrets
  * GitHub Actions OIDC

### Physical Hosts

* [Proxmox VE](./docs/proxmox/ve/setup)
  * network interfaces
  * terraform user
  * tailscale
* [Proxmox Backup Server](./docs/proxmox/backup-server/setup)

### Bootstrap VMs

* [OPNsense Firewall](./docs/opnsense/setup)
  * Interfaces:
    * WAN (vmbr0)
    * DMZ (vmbr1)
  * unbound DNS
  * DHCP w/ DNS registration
  * tailscale
* [Apt-Cacher-Ng Server](./docs/apt-cache/setup)
  * DMZ static IP .2
* [Infisical Server](./docs/infisical/self-hosted/setup) (if not using cloud version)
  * tailscale
  * common secrets
  * GitHub Actions OIDC

## Docker Compose template

TODO
