# Proxmox VE

Proxmox is the hypervisor that runs pretty much everything in my homelab. There are some things that need to be configured in Proxmox to get the infrastructure started.

## Network interfaces

When Proxmox VE was set up, it should have created a Linux Bridge `vmbr0` bound to a physical Network Device on the server.

Create an additional [OVS Bridge](https://pve.proxmox.com/wiki/Open_vSwitch) interface called `vmbr1` that will serve as an OPNsense LAN interface. When creating `vmbr1`, add the comment "OPNsense DMZ", click "Create", and then "Apply Configuration".

## terraform user

I use Terraform to provision resources in Proxmox, and I grant it access to PVE through a non-root account.

To set up the user, go to Datacenter > Permissions > Users, and create a pam user called "terraform".

Next, go to Datacenter > Permissions > API Tokens, and create an API token for the terraform user. Save the token secret to add to [common secrets](/docs/infisical/common-secrets) later.

## tailscale

Log into the pve console as root, and install the [tailscale](tailscale.com) client on the Proxmox host. Once installed, run the following commands to connect pve to the tailnet, enable the tailscale SSH server, and serve the Proxmox VE web ui on the tailnet:

```bash
tailscale up --ssh
tailscale serve --bg=true https+insecure://localhost:8006
```
