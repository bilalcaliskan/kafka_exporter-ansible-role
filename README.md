## Role Name

Installs and configures Kafka Exporter daemon on RHEL/CentOS 7/8 servers.

## Requirements

Requires a running kafka service on the same host; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

      - hosts: all
        roles:
          - role: bilalcaliskan.node_exporter
            become: yes

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

        kafka_port: 9092
        exporter_port: 9308
        exporter_type: kafka
        version: 1.2.0
        download_url: "https://github.com/danielqsj/kafka_exporter/releases/download/v{{ exporter_version }}/kafka_exporter-{{ exporter_version }}.linux-amd64.tar.gz"
        base_dir_path: /opt
        folder_path: "{{ base_dir_path }}/{{ exporter_type }}_exporter-{{ exporter_version }}.linux-amd64"
        file_path: "{{ base_dir_path }}/{{ exporter_type }}_exporter-{{ exporter_version }}.linux-amd64.tar.gz"
        user: prometheus
        group: prometheus
        user_login: /sbin/nologin

## Dependencies

None

## Example Playbook

      - hosts: all
        become: yes
        roles:
          - { role: bilalcaliskan.kafka_exporter }

*Inside `vars/main.yml`*:

        kafka_port: 9092
        exporter_port: 9308
        exporter_type: kafka
        version: 1.2.0
        download_url: "https://github.com/danielqsj/kafka_exporter/releases/download/v{{ exporter_version }}/kafka_exporter-{{ exporter_version }}.linux-amd64.tar.gz"
        base_dir_path: /opt
        folder_path: "{{ base_dir_path }}/{{ exporter_type }}_exporter-{{ exporter_version }}.linux-amd64"
        file_path: "{{ base_dir_path }}/{{ exporter_type }}_exporter-{{ exporter_version }}.linux-amd64.tar.gz"
        user: prometheus
        group: prometheus
        user_login: /sbin/nologin

## License

MIT / BSD
