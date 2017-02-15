# Ansible Role: nginx

An Ansible role that installs nginx on Fedora.

## Requirements

For configuring the firewall the service `firewalld` has to run and the package `python-firewall` needs to be installed.

## Role Variables

Available variables are listed below, along with default values:

    nginx_vhosts: []
    nginx_firewall_zones: []

### Virtual hosts

A list of virtual hosts can be configured with the variable `nginx_vhosts`.
Possible values for each entry in `nginx_vhosts` are, along with default values:

    name: ~
    listen: 80
    server_name: ~
    root: ~
    index: index.html
    error_page: ~
    access_log: ~
    error_log: ~
    extra_parameters: ~

#### Name

The `name` is used for the name of the file which will be created.

#### Host

The virtual host will be available under the server name defined in `server_name` and port defined in `listen`.

#### Document root

The document root can be configured in `root`, along with the default index file in `index`.

#### Error page

A custom error page can be set in `error_page`.

#### Logging

The keys `access_log` and `error_log` can be used to configure the location of log files.

#### Custom configuration

If you need more configuration for a virtual host, this can be defined in `extra_parameters` as a string, for example:

        nginx_vhosts:
          - name: example
            listen: 80
            server_name: example.com
            root: /var/www/example.com
            extra_parameters: |
                              location / {
                                try_files $uri foo/$uri;
                              }

### Firewall

The variable `nginx_firewall_zones` can be used to declare firewall zones in which nginx should be accessible.
This means the ports `80/tcp` and `443/udp` will be opened.

Currently only `firewalld` is supported which is default on Fedora.

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
