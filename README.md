# ansible-jtimon

## Description

Installs [jtimon](https://github.com/nileshsimaria/jtimon/), JunOS Telemetry Interface client.

## Requirements

Ansible >= 2.7 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

Name|Default Value|Description
---|---|---
`jtimon_version`|2.2.1|The jtimon version to be fetched from the [release page](https://github.com/nileshsimaria/jtimon/releases)
`jtimon_user`|jtimon|The linux user & group to setup on the target system for running jtimon.
`jtimon_bin`|/usr/local/bin|The location of the jtimon binary on the targets.
`jtimon_etc`|/etc/jtimon|The location of the jtimon config on the targets.
`jtimon_cli_flags`|-|CLI flags to be passed to the binary on start. See [defaults](defaults/main.yml) for example.
`jtimon_config_hosts`|{}|The config parameters which are used to create the `config-host.json` config file per host. See below or [defaults](defaults/main.yml) for example.

## Example Playbook

```yaml
- hosts: all
  become: true

  roles:
    - role: noris-network.ansible-jtimon
      vars:
        jtimon_config_hosts:
          - host: router1.fqdn.de
            port: 50051
            paths:
              - path: "/interfaces"
                freq: 4000
              - path: "/components"
                freq: 4000
          - host: router2.fqdn.de
            port: 50051
            paths:
              - path: "/interfaces"
                freq: 4000
```

## License

This project is licensed under Apache 2.0 License. See [LICENSE](LICENSE) for more details.

## Authors

- [Alexander Knipping](https://github.com/obitech)
- [Daniel Paufler](https://github.com/egmont1227)