Deploy AdGuard
=========
> This repository is only a mirror. Development and testing is done on a private gitlab server.

This role install and configure adguard, with optionally virtual IP, metrics, and consul integration on **debian-based** distributions.

Requirements
------------

This role assumes you have `docker`, `docker-compose`, and eventually `consul` installed if using the consul integration. The role will not install these components, but you can install them using the [install_docker](https://github.com/ednxzu/install_docker) and [hashicorp_consul](https://github.com/ednxzu/hashicorp_consul) roles.

Role Variables
--------------
Available variables are listed below, along with default values. A sample file for the default values is available in `default/deploy_adguard.yml.sample` in case you need it for any `group_vars` or `host_vars` configuration.

```yaml
deploy_adguard_directory: /opt/adguard # by default, set to /opt/adguard
```
This variable defines the data directory used to store all files related to adguard, as well as the volumes mounted by the docker containers.

```yaml
deploy_adguard_timezone: "Europe/Paris" # by default set to Europe/Paris
```
This variable defines the timezone that the container will use.

```yaml
deploy_adguard_enable_admin_interface: true #by default, set to true
```

```yaml
deploy_adguard_enable_dhcp: false # by default, set to false
```
Whether or not this server will be used as a dhcp server. This manages the port forwarding to the adguard container.

```yaml
deploy_adguard_enable_doh: true # by default, set to true
```
Whether or not this server will use DNS-over-HTTPS. This manages the port forwarding to the adguard container.

```yaml
deploy_adguard_enable_dot: false # by default, set to false
```
Whether or not this server will use DNS-over-TLS. This manages the port forwarding to the adguard container.

```yaml
deploy_adguard_enable_doq: false # by default, set to false
```
Whether or not this server will use DNS-over-QUIC. This manages the port forwarding to the adguard container.

```yaml
deploy_adguard_enable_dnscrypt: false # by default, set to false
```
Whether or not this server will use dnscrypt. This manages the port forwarding to the adguard container.


```yaml
deploy_adguard_start_service: false # bydefault, set to false
```
This variable manages whether or not to start the adguard service during the play, or when config files are changed. This can be useful to disable it if you plan on building golden images with this role and you don't want the containers to start during the build process. Please note that the service will ALWAYS be enabled, meaning that it'll automatically start upon reboot of the host.

```yaml
deploy_adguard_virtual_ip: # by default, set to the following
  enable: false
  interface: eth0
  vip_addr: "192.168.1.53"
```
This variable handles the use of a virtual IP for the dns server. You can either choose to use the host IP address to serve DNs, or you can choose to attach a virtual IP to the server, so that replacing the underlying machine will not force you to change dns settings everywhere.

```yaml
deploy_adguard_node_exporter: # by default, set to the following
  enable: false
  protocol: http
  port: 80
  username: changeme
  password: changeme
  exporter_port: 9617
  interval: 10s
  log_limit: 10000
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
# calling the role inside a playbook with either the default or group_vars/host_vars
- hosts: servers
  roles:
    - ednxzu.deploy_adguard
```

License
-------

MIT / BSD

Author Information
------------------

This role was created by Bertrand Lanson in 2023.