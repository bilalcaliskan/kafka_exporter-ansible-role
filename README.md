## Kafka Exporter Ansible Role

[![CI](https://github.com/bilalcaliskan/kafka_exporter-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/kafka_exporter-ansible-role/actions?query=workflow%3ACI)

Installs and configures kafka-exporter to expose Kafka metrics to Prometheus on RHEL/CentOS 7/8 instances.

### Requirements

This role requires a Running Kafka process on the same server. You can set up a Kafka cluster using [bilalcaliskan.kafka](https://galaxy.ansible.com/bilalcaliskan/kafka) role.
Also note that this role requires root access, so either run it in a playbook with a global `become: true`, or invoke the role in your playbook like:

*If you have a running Kafka process on the same server*:
```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.kafka_exporter
```

*If you do not have a running Kafka process on the same server, it will setup Kafka, Zookeeper
and Kafka exporter sequentially*:
```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.kafka
    - role: bilalcaliskan.kafka_exporter
```

### Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role will ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to stop and disable `firewalld` service, please modify below variable as false when running playbook:  
> ```yaml  
> firewalld_enabled: false

### Dependencies

None

### Example Playbook File For Installation

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.kafka_exporter
      vars:
        kafka_port: 9092
        install_kafka_exporter: true
        kafka_version: 123.123
        version: 1.2.0
```

You can also override default variables inside [vars/main.yml](vars/main.yml)*:
```yaml
version: 123.123
```

### Example Playbook File For `Ununinstallation`

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.kafka_exporter
      vars:
        install_kafka_exporter: false
```

### License

MIT / BSD
