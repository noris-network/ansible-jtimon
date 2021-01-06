# ansible-jtimon

## Description

Installs [jtimon](https://github.com/nileshsimaria/jtimon/), JunOS Telemetry Interface client.

The role is tested on vagrant:

- Centos 7
- Centos 8
- Debian 9
- Debian 10
- Ubuntu 18.04
- Ubuntu 20.04

## Requirements

Ansible >= 2.7 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

Name|Default Value|Description
---|---|---
`jtimon_version`|2.2.1|The jtimon version to be fetched from the [release page](https://github.com/nileshsimaria/jtimon/releases)
`jtimon_user`|jtimon|The linux user & group to setup on the target system for running jtimon.
`jtimon_bin`|/usr/local/bin|The location of the jtimon binary on the targets.
`jtimon_etc`|/etc/jtimon|The location of the jtimon config on the targets.
`jtimon_port`|8090|The port jtimon should listen on. Used for firewall and cli_flags.
`jtimon_cli_flags`|-|CLI flags to be passed to the binary on start. See [defaults](defaults/main.yml) for example.
`jtimon_config_hosts`|[]|The config parameters which are used to create the `config-host.json` config file per host. See below or [role defaults](defaults/main.yml) for examples.
`jtimon_alias_content`||See [role variables](defaults/main.yml) for sane defaults.
`jtimon_alias_file`|"{{ jtimon_etc }}/aliases.txt"|The location of alias.txt file.

## Example Playbook

```yaml
- hosts: all
  become: true

  roles:
    - role: noris-network.ansible-jtimon
      vars:
        jtimon_config_hosts:
          - host: router1.fqdn.de
            # your remote port
            port: 50051
            # keep next 2 variables
            cid: "{{ ansible_fqdn }}"
            alias: "{{ jtimon_alias_file }}"
            paths:
              - path: "/interfaces"
                # data every 10sec
                freq: 10000
              - path: "/components"
                freq: 10000
          - host: router2.fqdn.de
            port: 50051
            cid: "{{ ansible_fqdn }}"
            alias: "{{ jtimon_alias_file }}"
            paths:
              - path: "/interfaces"
                freq: 10000
```

## License

This project is licensed under Apache 2.0 License. See [LICENSE](LICENSE) for more details.

## Authors

- [Alexander Knipping](https://github.com/obitech)
- [Daniel Paufler](https://github.com/egmont1227)
