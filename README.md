# OVH DynHost client for Docker

Docker container to automatically update DynHost records with your public IP address, for [OVH](https://www.ovh.com/world/domains/dns_management_service.xml) DNS.

## Usage

1 - [Create a DynHost user and configure a dynamic DNS record](https://docs.ovh.com/us/en/domains/hosting_dynhost/) for the domain of your choice.

2 - Using information from the previous step, run DynHost client container to continuously update your DNS record.

### Using docker compose.

```yaml
version: "3"

services:
  dynhost-updater:
    image: sylvanld/update-ovh-dynhost
    environment:
      HOSTNAME: "<host>.<domain>"
      IDENTIFIER: "<domain>-<suffix>"
      PASSWORD: "<password>"
      LOG_LEVEL: "debug"
```

### Using kubernetes

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: dynhost-updater
spec:
  containers:
    - name: dynhost-updater
      image: sylvanld/update-ovh-dynhost
      env:
        - name: HOSTNAME
          value: "<host>.<domain>"
        - name: IDENTIFIER
          value: "<domain>-<suffix>"
        - name: PASSWORD
          value: "<password>"
        - name: LOG_LEVEL
          value: "debug"
```

### Environment variables

|Variable|Description|Is required?|Default|
|-|-|-|-|
|HOSTNAME|Subdomain on which DNS record must be updated dynamically.|**Yes**|-|
|IDENTIFIER|DynHost management username.|**Yes**|-|
|PASSWORD|DynHost management password.|**Yes**|-|
|LOG_LEVEL|String used to configure verbosity (must be one of: 'debug', 'info', 'error')|No|debug|
