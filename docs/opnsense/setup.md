# OPNsense

OPNsense firewall provides network segmentation, DHCP, and DNS for my homelab. The following configurations are needed for my templates to work.

## Interface setup

The following interfaces need to be configured in OPNsense:

* vmbr0 -> WAN (static IP in WAN net)
* vmbr1 -> DMZ (10.0.0.1/24)
* vmbr2 -> ADMN (10.0.11.1/24)

## DHCP

ISC DHCPv4 must be configured for the DMZ and ADMN networks. Make sure the following settings are in place for each interface:

* Enable DHCP server on the interface
* Set range from .10 to .245
* Set DNS server to the OPNsense gateway IP for that interface (only 1 DNS server per interface)
    * DMZ -> 10.0.0.1
    * ADMN -> 10.0.11.1
* Set domain name to your internal domain
* Set domain search list to your internal domain

## DNS

Unbound DNS must be configured for DHCP DNS registration. Make sure the following settings are in place:

* Enable Unbound
* Register ISC DHCP4 Leases
* Set DHCP Domain Override to your internal domain

## tailscale

Follow [Tailscale's guide](https://tailscale.com/kb/1097/install-opnsense) to install tailscaled on OPNsense. Make sure you have at least 8GB of storage space available before installing tailscaled and its dependencies. It may take a while to build everything.

Once tailscale is installed, run the following commands to start the tailscaled service, join the tailnet, advertise a route to the DMZ, and serve the OPNsense web UI:

```bash
service tailscaled enable
service tailscaled start
tailscale up --hostname="opnsense" --advertise-tags="infrastructure" --advertise-routes="10.0.0.0/24"
tailscale serve --bg http://localhost:80
```
