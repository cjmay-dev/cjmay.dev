# Tailscale

Tailscale is the glue that allows my CI/CD pipeline to access parts of my infrastructure. It also allows me to do remote administration when I'm not on my home network.

## Access controls

I won't share the details of my access controls config, but the following is generally needed for my templates to work:

### Tags

* ci (ephemeral runners)
* infrastructure (proxmox, infisical)

### ACLs

* ci to infrastructure

### SSH

* ci to infrastructure

### Funnel

* default (owners can configure)

HTTPS certificates must also be enabled under DNS > HTTPS Certificates

## OAuth Client

The CI/CD pipeline needs an auth key to temporarily join the tailnet without an interactive logon. OAuth client credentials can be created under Settings > OAuth clients. Give the client a description and enable the following permissions:

* Auth Keys - R/W - tag:ci

![image](https://github.com/user-attachments/assets/3565024f-ffb2-4eaf-a74b-59b5ddda5be9)

Once the OAuth credentials are created, save them for later so they can be added to the Infisical [common secrets](/docs/infisical/common-secrets).

## Machines

The following machines need to be added to the tailnet for my templates to work. Use the provided links to see the tailscale setup documentation for each machine.

* [Proxmox](/docs/proxmox/ve/setup#tailscale)
* [OPNsense](/docs/opnsense/setup#tailscale)
* [Infisical](/docs/infisical/self-hosted/setup#tailscale) (if self-hosting)