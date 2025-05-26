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

OPNsense now includes an official plugin for tailscale called `os-tailscale` which needs to be installed. Once installed, go to the tailscale console.

In the tailscale console, generate an auth key for OPNsense under Settings > Keys. Give the auth key a description and add `infrastructure` as a default tag on the key.

Back in OPNsense, go to VPN > Tailscale > Authentication and add the generated key to the Pre-authentication Key field. Next, go to VPN > Tailscale > Settings. Enable Tailscale, disable "Accept DNS", and enable "Advertise Exit Node". Click the "Apply" button to join the tailnet.

Next, go to the "Advertised Routes" on the same page, and add the following routes:

* 10.0.0.0/24 (DMZ)

Click the "Apply" button again, and then go back to the tailscale console.

In the Machines tab of the tailscale console, locate opnsense, edit its route settings, and accept the route and exit node advertisements.

One more tailscale-related thing to configure in OPNsense is NAT-PMP. If there are any devices on OPNsense's LAN interfaces that are using tailscale, then [NAT-PMP must be enabled](https://tailscale.com/kb/1097/install-opnsense#nat-pmp) on those interfaces to allow direct connections. Without NAT-PMP, those devices can only use DERP relays.