# GCP Dynamic DNS
GCP Dynamic DNS updater from https://github.com/luontola/gcp-dynamic-dns.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_gcp_ddns/blob/main/meta/main.yml)

Requires a Service Account with DNS Administrator role.

1. Create Service Account (console.cloud.google.com):
    * IAM & admin ➔ Service accounts ➔ Create Service Account
        * Name: dns-updater
        * Service account ID: {GENERATE ID}
        * Description: Dynamic DNS updater.
        * Permissions: DNS Administrator
        * Principals with access: {SKIP}

2. Generate Keys (console.cloud.google.com):
    * Service accounts ➔ Dynamic DNS Updater ➔ ⋮ ➔ Manage Keys ➔ Add key
        * Key type: JSON

3. ansible-vault encrypt service_account.json

## Role Variables
[defaults](https://github.com/r-pufky/ansible_gcp_ddns/tree/main/defaults/main)

### Ports
No additional ports required.

## Dependencies
**galaxy-ng** roles cannot be used independently. Part of
[r_pufky.srv](https://github.com/r-pufky/ansible_collection_srv) collection.

## Example Playbook
Read defaults documentation.

### Pre-configured deployment
Service will automatically be restarted when configuration is defined.

``` yaml
- name: 'GCP DDNS updater'
  hosts: 'ddns.example.com'
  become: true
  roles:
     - 'r_pufky.srv.gcp_ddns'
  vars:
    gcp_ddns_cfg_dns_names:
      - 'example.com.'
      - 'subdomain.example.com.'
    gcp_ddns_cfg_google_project: 'example-project-123456789'
    gcp_ddns_srv_keys: 'host_vars/ddns.example.com/service_account_keys.json'
```

## Development
Configure [environment](https://r-pufky.github.io/ansible_collection_docs/ansible/environment)

Run all unit tests:
``` bash
molecule test --all
```

### Releases
Release format: **{OS}-{SERVICE}-{ROLE}**

Each type inherits the versioning system used; defaulting to schematic
versioning.

`12.0.0-2.0.3-1.0.0`

* 12.0.0 - Debian 12 (bookworm).
* 2.0.3 - Service/app version.
* 1.0.0 - Role version.

Releases are branched on Debian releases:

* **[13.x.x](https://github.com/r-pufky/ansible_gcp_ddns)**: 13 Trixie.
* **[12.x.x](https://github.com/r-pufky/ansible_gcp_ddns/tree/12.x)**: 12 Bookworm.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_gcp_ddns/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
