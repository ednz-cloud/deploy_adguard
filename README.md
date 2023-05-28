Deplou AdGuard
=========
> This repository is only a mirror. Development and testing is done on a private gitlab server.

This role install and configure adguard, with optionally virtual IP, metrics, and consul integration on **debian-based** distributions.

Requirements
------------

This role assumes you have `docker`, `docker-compose`, and eventually `consul` installed if using the consul integration. The role will not install these components, but you can install them using the [install_docker](https://github.com/ednxzu/install_docker) and [hashicorp_consul](https://github.com/ednxzu/hashicorp_consul) roles.

Role Variables
--------------
Available variables are listed below, along with default values. A sample file for the default values is available in `default/deploy_adguard.yml.sample` in case you need it for any `group_vars` or `host_vars` configuration.

Dependencies
------------

This role has a task that installs its own dependencies located in `task/prerequisites.yml`, so that you don't need to manage them. This role requires both `ednxzu.manage_repositories` and `ednxzu.manage_apt_packages` to install consul.

Example Playbook
----------------

```yaml
# calling the role inside a playbook with either the default or group_vars/host_vars
- hosts: servers
  roles:
    - ednxzu.hashicorp_consul
```

License
-------

MIT / BSD

Author Information
------------------

This role was created by Bertrand Lanson in 2023.