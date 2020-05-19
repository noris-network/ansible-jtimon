# ansible-jtimon

## Description

Installs [jtimon](https://github.com/nileshsimaria/jtimon/), JunOS Telemetry Interface client.

## Requirements

- Ansible >= 2.7 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

Name|Default Value|Description
---|---|---
`jtimon_user`|jtimon|The linux user & group to setup on the target system for running jtimon.
`jtimon_version`|2.2.1|The jtimon version to be fetched from the [release page](https://github.com/nileshsimaria/jtimon/releases)
`jtimon_bin`|/usr/local/bin|The location of the jtimon binary on the targets.
`jtimon_cli_flags`|{}|CLI flags to be passed to the binary on start. See [defaults](defaults/main.yml) for example.
`jtimon_config`|{}|The config parameters which are used to create the `jtimon.json` config file. See [defaults](defaults/main.yml) for example.

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - noris-network.jtimon
```

## License


This project is licensed under Apache 2.0 License. See [LICENSE](LICENSE) for more details.
