
williamyeh.fluentd for Ansible Galaxy
============


## Summary

Role name in Ansible Galaxy: **[williamyeh.fluentd](https://galaxy.ansible.com/list#/roles/2269)**

This Ansible role has the following features for [Fluentd](http://www.fluentd.org/):

 - Install td-agent: the stable distribution of Fluentd.
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
```



## Handlers

- `restart td-agent`

- `stop td-agent`




## Usage


### Step 1: add role

Add role name `williamyeh.fluentd` to your playbook file.


### Step 2: add variables

Set vars in your playbook file.

Simple example:

```yaml
---
# file: simple-playbook.yml

- hosts: all

  roles:
    - williamyeh.fluentd
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
      - fluent-plugin-elasticsearch
      - fluent-plugin-kafka

  tasks:
    - name: Copy project-specific config file for Fluentd 
      template: src=templates/td-agent.conf.j2  dest=/etc/td-agent/td-agent.conf
      notify:
        - restart td-agent
```


## Dependencies

None.


## License

Licensed under the Apache License V2.0. See the [LICENSE file](LICENSE) for details.


## History

Modified from my Dockerized Fluentd app:

  - [williamyeh/fluentd](https://github.com/William-Yeh/docker-fluentd)
