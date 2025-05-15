# Foundational Infisical secrets

The IaC in my various deployment templates need secure access to various secrets to set up things like:

* container hosts
* immutable backup storage buckets
* cloudflare tunnels

These are the secrets that need to be set up to use my templates:

| Secret Name | Description | Required Permissions |
| --- | --- | --- |
| BACKUPS/BACKBLAZE_B2_KEY_ID | App key to create backup buckets | listAllBucketNames, listBuckets, readBuckets, writeBuckets, listKeys, writeKeys, deleteKeys, readBucketEncryption, writeBucketEncryption, readBucketRetentions, writeBucketRetentions |
| BACKUPS/BACKBLAZE_B2_KEY_SECRET | App secret to create backup buckets | listAllBucketNames, listBuckets, readBuckets, writeBuckets, listKeys, writeKeys, deleteKeys, readBucketEncryption, writeBucketEncryption, readBucketRetentions, writeBucketRetentions |
| BACKUPS/RESTIC_BACKUP_PASSWORD | Password used to encrypt backups | N/A |
| BACKUPS/STACKBACK_DISCORD_WEBHOOK | Webhook for backup notifications | N/A |
| CLOUDFLARE/CLOUDFLARE_ACCOUNT_ID | Cloudflare account ID | N/A |
| CLOUDFLARE/CLOUDFLARE_API_TOKEN | API token to set up cloudflare tunnel | Account.Cloudflare_Tunnel:Edit, Zone.DNS:Edit |
| CLOUDFLARE/CLOUDFLARE_DOMAIN | The Cloudflare domain being deployed to | N/A |
| CLOUDFLARE/CLOUDFLARE_ZONE_ID | Zone ID of the Cloudflare domain | N/A |
| INFISICAL/INFISICAL_ADMIN_USER | Email of the Infisical admin user | N/A |
| PROXMOX/ADMIN_USERNAME | Username for admin user on Linux VMs | N/A |
| PROXMOX/ADMIN_SSH_PUBLIC_KEY | SSH pubkey for admin user on Linux VMs | N/A |
| PROXMOX/ANSIBLE_SSH_PUBLIC_KEY | SSH pubkey for ansible user on Linux VMs | N/A |
| PROXMOX/DATASTORE_ID | Name of the Proxmox datastore for VM storage | N/A |
| PROXMOX/PROXMOX_VE_API_TOKEN | API token for Proxmox Terraform user | TODO |
| PROXMOX/PROXMOX_VE_ENDPOINT | HTTPS endpoint for the Proxmox web UI | N/A |
| PROXMOX/PROXMOX_VE_INSECURE | Whether Proxmox HTTPS cert is self-signed | N/A |
| PROXMOX/PROXMOX_VE_SSH_KEY | SSH key for Proxmox Terraform user | TODO |
| TAILSCALE/TS_OAUTH_CLIENT_ID | OAuth client ID for joining tailnet | N/A |
| TAILSCALE/TS_OAUTH_SECRET | OAuth client secret for joining tailnet | N/A |
| TFSTATE/AWS_ACCESS_KEY_ID | Access key to Terraform state storage bucket | listBuckets, readObjects, writeObjects, deleteObjects |
| TFSTATE/AWS_SECRET_ACCESS_KEY | Access key to Terraform state storage bucket | listBuckets, readObjects, writeObjects, deleteObjects |
| TFSTATE/TFSTATE_BUCKET | S3 URI for tfstate bucket | N/A |
| TFSTATE/TFSTATE_BUCKET_REGION | S3 region for tfstate bucket | N/A |
