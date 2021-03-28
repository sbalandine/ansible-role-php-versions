# Ansible Role: PHP Versions

Allows different PHP versions to be installed when using the `sbalandine.php` role (or a similar role). This role was originally built for [Drupal VM](https://www.drupalvm.com) but was released more generically so others could use an easier mechanism for switching PHP versions.

## Requirements

N/A

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    php_version: '7.4'

The PHP version to be installed. Any [currently-supported PHP major version](http://php.net/supported-versions.php) is a valid option (e.g. `7.3`, `7.4`, or `8.0`).

    php_versions_install_recommends: false

(For Debian OSes only) Whether to install recommended packages. This is set to `no` by default because setting it to `yes` often leads to multiple PHP versions being installed (thus making a bit of a mess) when using repos like Ondrej's PHP PPA for Ubuntu.

## Dependencies

  - sbalandine.php is a soft dependency as the `php_version` variable is required to be set.
  - sbalandine.repo-remi, if you're using CentOS or a Red Hat derivative.

## Example Playbook

    - hosts: webservers
      become: true
    
      vars:
        php_version: '7.4'
    
      roles:
        - name: sbalandine.repo-remi
          when: ansible_os_family | lower == 'redhat'
        - sbalandine.php-versions
        - sbalandine.php

## License

MIT / BSD

## Author Information

This role was created in 2017 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/) and adapted by Serge Balandine.

