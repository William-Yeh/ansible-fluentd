
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

Variables needed to be defined in user's playbook: None.


### Optional variables

User-configurable defaults:

```yaml
# an array of plugins to be installed
tdagent_plugins

# conf file (usually td-agent.conf) to be installed,
# relative to `playbook_dir`;
# the file will be copied verbatim
tdagent_conf_copy

# conf file (usually td-agent.conf.j2) to be installed,
# relative to `playbook_dir`;
# the file will be copied through Ansible's template system
tdagent_conf_template
```



## Handlers

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
      - fluent-plugin-flowcounter
      - fluent-plugin-elasticsearch
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
```


## Dependencies

None.


## License

Licensed under the MIT License. See the [LICENSE file](LICENSE) for details.


## History

Modified from my Dockerized Fluentd app:

  - [williamyeh/fluentd](https://github.com/William-Yeh/docker-fluentd)
