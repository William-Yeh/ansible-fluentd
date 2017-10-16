<a href="https://www.fluentd.org">
    <img src="https://www.fluentd.org/assets/img/miscellany/fluentd-logo.png" alt="fluentd logo" title="fluentd" align="right" height="60" />
</a>

Ansible Role: fluentd
=====================

[![Build Status](https://travis-ci.org/SoInteractive/ansible-fluentd.svg?branch=master)](https://travis-ci.org/SoInteractive/ansible-fluentd) [![License: MIT](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT) [![Ansible Role](http://img.shields.io/badge/ansible%20role-SoInteractive.fluentd-blue.svg)](https://galaxy.ansible.com/SoInteractive/fluentd/) [![GitHub tag](https://img.shields.io/github/tag/sointeractive/ansible-fluentd.svg)](https://github.com/SoInteractive/ansible-fluentd/tags) [![Twitter URL](https://img.shields.io/twitter/follow/sointeractive.svg?style=social&label=Follow%20%40SoInteractive)](https://twitter.com/sointeractive)

Role installs fluentd log forwarder and agregator

Examples
--------

Use it in a playbook as follows:
```yaml
- hosts: all
  become: true
  roles:
    - SoInteractive.fluentd
```

Have a look at the [defaults/main.yml](defaults/main.yml) for role variables
that can be overridden.
