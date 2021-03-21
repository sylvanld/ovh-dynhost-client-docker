# OVH DynHost client for Docker

Docker container to automatically update DynHost records with your public IP address, for [OVH](https://www.ovh.com/world/domains/dns_management_service.xml) DNS.

## Usage

1 - [Create a DynHost user and configure a dynamic DNS record](https://docs.ovh.com/us/en/domains/hosting_dynhost/) for the domain of your choice.

2 - Using information from the previous step, run DynHost client container to continuously update your DNS record.

E.G using docker compose.

*compose file*
```yaml
version: "3"

services:
  dynhost-updater:
    image: sylvanld/update-ovh-dynhost
    environment:
      HOSTNAME: "<host>.<domain>"
      IDENTIFIER: "<domain>-<suffix>"
      PASSWORD: "<password>"
```

*Following environment variables are mandatory* :
- **HOSTNAME**: Subdomain on which DNS record must be updated dynamically.
- **IDENTIFIER**: DynHost management username.
- **PASSWORD**: DynHost management password.
