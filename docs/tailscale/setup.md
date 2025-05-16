# Tailscale

Tailscale is the glue that allows my CI/CD pipeline to access the private parts of my network. It also allows me to do remote administration when I'm not on my home network.

## Access controls

I won't share the details of my access controls config, but the following is generally needed for my templates to work:

### Tags

* ci
* infrastructure
* services

### ACLs

* ci to infrastructure
* ci to services

### SSH

* ci to infrastructure

### Funnel

* default / owners can configure

HTTPS certificates must also be enabled under DNS > HTTPS Certificates

## OAuth Client

My CI/CD pipeline needs an auth key to join devices to my tailnet without an interactive logon. OAuth client credentials can be created under Settings > OAuth clients. Give the client a description and enable the following permissions:

* Auth Keys - R/W - tag:ci,tag:services

![image](https://github.com/user-attachments/assets/3565024f-ffb2-4eaf-a74b-59b5ddda5be9)

Once the OAuth credentials are created, save them for later so they can be added to the Infisical [common secrets](/docs/infisical/common-secrets).
