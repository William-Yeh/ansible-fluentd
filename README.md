
williamyeh.fluentd for Ansible Galaxy
============


[![Circle CI](https://circleci.com/gh/William-Yeh/ansible-fluentd.svg?style=shield)](https://circleci.com/gh/William-Yeh/ansible-fluentd) [![Build Status](https://travis-ci.org/William-Yeh/ansible-fluentd.svg?branch=master)](https://travis-ci.org/William-Yeh/ansible-fluentd)


## Summary

Role name in Ansible Galaxy: **[williamyeh.fluentd](https://galaxy.ansible.com/williamyeh/fluentd/)**

This Ansible role has the following features for [Fluentd](http://www.fluentd.org/):

 - Install [td-agent](https://docs.treasuredata.com/articles/td-agent): the stable Fluentd distribution package maintained by [Treasure Data, Inc](https://www.treasuredata.com/).
 - Install several plugins.
 - Bare bone configuration (*real* configuration should be left to user's template files; see **Usage** section below).



## Role Variables

### Mandatory variables

None.


### Optional variables

User-configurable defaults:

```yaml
# td-agent version; e.g., 2.3.4
# Will install the default (usually the latest stable) version, if not specified.
tdagent_version


# an array of plugins (with latest versions) to be installed
tdagent_plugins

# an dict of plugins (with specified versions) to be installed
# dict fields:
#   - key: memo for this plugin
#   - value:
#     - name:    plugin name
#     - version: plugin version
tdagent_plugins_versions
```

User-installable configuration files - main configuration:

```yaml
# conf file (usually td-agent.conf) to be installed,
# relative to `playbook_dir`;
# the file will be copied verbatim
tdagent_conf_copy

# conf file (usually td-agent.conf.j2) to be installed,
# relative to `playbook_dir`;
# the file will be copied through Ansible's template system
tdagent_conf_template
```

User-installable configuration files - other configurations:

```yaml
# other conf templates to be installed to "/etc/td-agent/conf.d";
# dict fields:
#   - key: memo for this conf
#   - value:
#     - src:  template file relative to `playbook_dir`
#     - dest: target file relative to `/etc/td-agent/conf.d/`
tdagent_conf_others
```



## Handlers

- `reload td-agent`

- `restart td-agent`

- `stop td-agent`




## Usage


### Step 1: add role

Add role name `williamyeh.fluentd` to your playbook file.


### Step 2: add variables, if any

Set vars in your playbook file.

Simple example:

```yaml
---
# file: simple-playbook.yml

- hosts: all

  roles:
    - williamyeh.fluentd

  vars:
    tdagent_plugins:
      - fluent-plugin-multiprocess
      - fluent-plugin-forest
      - fluent-plugin-elasticsearch

    tdagent_plugins_versions:
      prometheus:
        name: fluent-plugin-prometheus
        version: 0.1.2
      flowcounter:
        name: fluent-plugin-flowcounter
        version: 0.4.1

```


### Step 3: copy user's config file, if necessary


More practical example:

```yaml
---
# file: complex-playbook.yml

- hosts: all

  roles:
    - williamyeh.fluentd

  vars:
    tdagent_plugins:
      - fluent-plugin-multiprocess
      - fluent-plugin-flowcounter
      - fluent-plugin-elasticsearch

    # copy verbatim
    tdagent_conf_copy: "files/td-agent.conf"

    # copy through Ansible's template system
    tdagent_conf_template: "templates/td-agent.conf.j2"

    # other configurations to be copied through Ansible's template system
    tdagent_conf_others:
      prometheus_metrics:
        src:  templates/prometheus.conf.j2
        dest: prometheus.conf
```


## Dependencies

None.


## License

Licensed under the MIT License. See the [LICENSE file](LICENSE) for details.


## History

Modified from my Dockerized Fluentd app:

  - [williamyeh/fluentd](https://github.com/William-Yeh/docker-fluentd)
