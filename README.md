# [GCP Dynamic DNS][h]
GCP Dynamic DNS updater from source.

## [Requirements][i]
Requires [r_pufky.srv][g] galaxy-ng collection. See
[reference documentation][h] for troubleshooting and config variables.

Install size: ~132MB

## Role Variables
Detailed variable use documented in defaults. See usage for role operation.

* [defaults][j] - User configurable options.

## Usage
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

### Feature Flags
Tasks are gated by feature flags and executed in the following order.

  Step | Flag                     | Notes
 ------|--------------------------|-------
  1    | gcp_ddns_flg_maintenance | Preform role maintenance tasks.
  2    | gcp_ddns_flg_install     | Install required packages, users, etc.
  3    | gcp_ddns_flg_config      | Install user-defined config.

### Example Playbooks

#### Pre-configured deployment

``` yaml
- name: 'Deploy GCP DDNS.'
  ansible.builtin.include_role:
    name: 'r_pufky.srv.gcp_ddns'
  vars:
    gcp_ddns_srv_keys: 'host_Vars/ddns.example.com/data/service_account.json'
    gcp_ddns_cfg_dns_names:
      - 'example.com.'
      - 'subdomain.example.com.'
    gcp_ddns_cfg_google_project: 'example-project-123456789'
```

## Development
Configure [environment][a].

``` bash
# Run all tests.
molecule test --all
```

Testing variables:

  Variable            | type | Description
 ---------------------|------|-------------
  molecule_flg_test   | bool | Flag for generic test signal (disables GCP query).

### [Releases][b]

  Release | Debian | Ansible | GCP DDNS | Notes
 ---------|--------|---------|----------|-------
  1.x.x   | 13     | 2.20    | v1.5     | Ansible 2.20, feature flags, and semantic versioning.
  0.x.x   | 13     | 2.18    | v1.5     | Initial release.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License][c] | [direct link][f]

## Author Information
PGP: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9][d] | [github gist][e]

[a]: https://r-pufky.github.io/ansible_docs
[b]: https://semver.org/spec/v2.0.0
[c]: https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0
[d]: https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9
[e]: https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22

[f]: https://github.com/r-pufky/ansible_gcp_ddns/blob/main/LICENSE
[g]: https://github.com/r-pufky/ansible_collection_srv
[h]: https://github.com/luontola/gcp-dynamic-dns
[i]: https://github.com/r-pufky/ansible_gcp_ddns/blob/main/meta/main.yml
[j]: https://github.com/r-pufky/ansible_gcp_ddns/tree/main/defaults/main/main.yml