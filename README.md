# ansible-role-acme-cf

## Description

Ansible role to generate wildcard SSL certificates using DNS-01 challenge via [Cloudflare](https://cloudflare.com).

## Usage

### Installation

```bash
ansible-galaxy install ndkprd.acme_cf
```

### Hosts Example

```yaml
---

# hosts.yaml

acme_cf_domains:
  hosts:
    dev.example.com:
      domain: dev.example.com
      domain_alias_enabled: true
      domain_alias_zone: example.xyz
      domain_alias_record: "_acme-challenge"
    stg.example.com:
      domain: stg.example.com
      domain_alias_enabled: true
      domain_alias_zone: example.xyz
      domain_alias_record: "_acme-challenge"
    devops.example.com:
      domain: devops.example.com
      domain_alias_enabled: true
      domain_alias_zone: example.xyz
      domain_alias_record: "_acme-challenge"
    itops.example.com:
      domain: itops.example.com
      domain_alias_enabled: true
      domain_alias_zone: example.xyz
      domain_alias_record: "_acme-challenge"
    example.io:
      domain: example.io
      domain_alias_enabled: true
      domain_alias_zone: example.xyz
      domain_alias_record: "_acme-challenge"
    example.link:
      domain: example.link
      domain_alias_enabled: true
      domain_alias_zone: example.xyz
      domain_alias_record: "_acme-challenge"
    example.xyz:
      domain: example.xyz
      domain_alias_enabled: true
      domain_alias_zone: example.xyz
      domain_alias_record: "_acme-challenge"
```

### Playbook Example

```yaml
---

- name: Generate SSL certificates using ACME DNS-01 challenge.
  hosts: acme_cf_domains
  connection: local
  become: false
  gather_facts: false
  vars:
    acme_cf_files_dir: "/home/ndkprd/.ssl/acme"
    acme_cf_server_dir: "https://acme-staging-v02.api.letsencrypt.org/directory"
    acme_cf_remaining_days: 30
    acme_cf_account_email: andhika.pradana@asdp.id
    acme_cf_api_token: "{{ lookup('ansible.builtin.env', 'CLOUDFLARE_API_TOKEN') }}"
    acme_cf_alias_enabled: true
    acme_cf_alias_zone: "asdp.my.id"
    acme_cf_alias_record: "_acme-challenge"
  roles:
    - ndkprd.acme_cf
```

The generated files will be located in the dir you set in `acme_cf_files_dir` var, with the default being `/tmp/acme_cf`.

## Notes

There's some tasks that is tagged with `debug` tag that is basically just print out variable vars for debugging purpose. You can skip those using `--skip-tags=debug` flag.

## TODO

- [x] add support for non-aliases/CNAME delegation;
- [x] change input from string to list so it can be used for multiple domains at once;
- [ ] Add checksums.

## License

[MIT](./LICENSE)
