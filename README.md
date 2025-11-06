# ansible-role-acme-cf

## Description

Ansible role to generate wildcard SSL certificates using DNS-01 challenge via [Cloudflare](https://cloudflare.com).

## Usage

### Installation

```bash
ansible-galaxy install ndkprd.acme_cf
```

### Hosts Example

See [examples/hosts.yaml](./examples/hosts.yaml).

### Playbook Example

See [examples/playbook.yaml](./examples/playbook.yaml).

The generated files will be located in the dir you set in `acme_cf_files_dir` var, with the default being `/tmp/ansible/acme_cf/<domain_name>`.

## Notes

There's some tasks that is tagged with `debug` tag that is basically just print out variable vars for debugging purpose. You can skip those using `--skip-tags=debug` flag.

## TODO

- [x] add support for non-aliases/CNAME delegation;
- [x] change input from string to list so it can be used for multiple domains at once;
- [ ] Add checksums.

## License

[MIT](./LICENSE)
