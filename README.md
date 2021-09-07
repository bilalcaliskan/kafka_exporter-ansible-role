# Kafka Exporter Ansible Role

[![CI](https://github.com/bilalcaliskan/kafka_exporter-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/kafka_exporter-ansible-role/actions?query=workflow%3ACI)

Installs and configures [kafka-exporter](https://github.com/danielqsj/kafka_exporter) on Redhat/Debian based hosts.

If you need also Kafka, please refer to [bilalcaliskan.kafka](https://github.com/bilalcaliskan/kafka-ansible-role).

## Requirements

This role requires minimum Ansible version 2.4 and maximum Ansible version 2.9. You can install suggested version with pip:
```
$ pip install "ansible==2.9.16"
```

This role requires a Running Kafka process on the same server. You can set up a Kafka cluster using [bilalcaliskan.kafka](https://galaxy.ansible.com/bilalcaliskan/kafka) role.
Also note that this role requires root access, so either run it in a playbook with a global `become: true`, or invoke the role in your playbook.


## Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role will ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to stop and disable `firewalld` service, please modify below variable as false when running playbook:
> ```yaml
> firewalld_enabled: false

## Dependencies

None

## Examples
### Inventory
```
[all]
broker01.example.com
broker02.example.com
broker03.example.com
```

### Installation

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.kafka_exporter
      vars:
        kafka_port: 9092
        exporter_port: 9308
        install_kafka_exporter: true
        kafka_version: 123.123
        version: 1.2.0
```

### Uninstallation

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.kafka_exporter
      vars:
        install_kafka_exporter: false
```

## Development
This project requires below tools while developing:
- [Ansible 2.4 or higher](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [pre-commit](https://pre-commit.com/)
- [ansible-lint](https://ansible-lint.readthedocs.io/en/latest/installing.html#using-pip-or-pipx) - required by [pre-commit](https://pre-commit.com/)
- [Bash shell](https://www.gnu.org/software/bash/) - required by [pre-commit](https://pre-commit.com/)

## License

Apache License 2.0
