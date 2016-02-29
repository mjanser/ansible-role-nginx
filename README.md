# Ansible Role: nginx

An Ansible role that installs nginx on Fedora.

## Requirements

For configuring the firewall the service `firewalld` has to run and the package `python-firewall` needs to be installed.

## Role Variables

Available variables are listed below, along with default values:

    nginx_vhosts: []
    nginx_firewall_zones: []

Possible values for `nginx_vhosts` entries are, along with default values:

    name: ~
    listen: 80
    server_name: ~
    root: ~
    index: index.html
    error_page: ~
    access_log: ~
    error_log: ~
    extra_parameters: ~

## Dependencies

None

## Example Playbook

    - hosts: all
      roles:
        - { role: mjanser.nginx }
      vars:
        nginx_vhosts:
          - name: example
            listen: 80
            server_name: example.com
            root: /var/www/example.com

## License

MIT
