## Kafka Exporter Ansible Role

[![Build Status](https://travis-ci.com/bilalcaliskan/kafka_exporter-ansible-role.svg?branch=master)](https://travis-ci.com/bilalcaliskan/kafka_exporter-ansible-role)

Installs and configures kafka-exporter to expose Kafka metrics to Prometheus on RHEL/CentOS 7/8 instances.

## Requirements

This role requires a Running Kafka process on the same server. You can set up a Kafka cluster using bilalcaliskan.kafka role.
Also note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role
in your playbook like:

*If you have a running Kafka process on the same server*:

      - hosts: all
        become: true
        roles:
          - role: bilalcaliskan.kafka_exporter

*If you do not have a running Kafka process on the same server*:

      - hosts: all
        become: true
        roles:
          - role: bilalcaliskan.kafka
          - role: bilalcaliskan.kafka_exporter

## Role Variables

See the default values in 'defaults/main.yml'. You can overwrite them in 'vars/main.yml' if neccessary.

## Dependencies

None

## Example Playbook

      - hosts: all
        become: true
        vars_files:
          - vars/main.yml
        roles:
          - role: bilalcaliskan.kafka_exporter

*Inside `vars/main.yml`*:

        kafka_port: 9092
        exporter_port: 9308
        exporter_type: kafka
        version: 1.2.0
        download_url: "https://github.com/danielqsj/kafka_exporter/releases/download/v{{ version }}/kafka_exporter-{{ version }}.linux-amd64.tar.gz"
        base_dir_path: /opt
        folder_path: "{{ base_dir_path }}/{{ exporter_type }}_exporter-{{ version }}.linux-amd64"
        file_path: "{{ base_dir_path }}/{{ exporter_type }}_exporter-{{ version }}.linux-amd64.tar.gz"
        user: kafka-exporter
        group: kafka-exporter
        user_login: /sbin/nologin

## Playbook for uninstall

      - hosts: all
        become: true
        vars_files:
          - vars/main.yml
        roles:
          - role: bilalcaliskan.kafka_exporter

*Inside `vars/main.yml`*:

        install_kafka_exporter: false

## License

MIT / BSD
