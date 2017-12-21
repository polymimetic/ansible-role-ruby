# Ansible Role: Ruby

[![Build Status](https://img.shields.io/travis/polymimetic/ansible-role-ruby.svg?style=flat-square)](https://travis-ci.org/polymimetic/ansible-role-ruby)
[![Release](https://img.shields.io/github/tag/polymimetic/ansible-role-ruby.svg?style=flat-square)](https://github.com/polymimetic/ansible-role-ruby/releases)
[![License: MIT](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-polymimetic.ruby-blue.svg?style=flat-square)](https://galaxy.ansible.com/polymimetic/ruby/)

Installs Ruby and bundler gem on Linux.

## Requirements

No requirements.

## Dependencies

No dependencies.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    ruby_workspace: /root

The location where temporary files will be downloaded in preparation for Ruby installation.

    ruby_user: username

The user account under which Ruby gems will be installed. Defaults to the `ansible_ssh_user` if not set.

    ruby_dependencies:
      - git-core
      - curl
      - zlib1g-dev
      - build-essential
      - libssl-dev
      - libreadline-dev
      - libyaml-dev
      - libsqlite3-dev
      - sqlite3
      - libxml2-dev
      - libxslt1-dev
      - libcurl4-openssl-dev
      - python-software-properties
      - libffi-dev

Build dependencies for packages (will be installed with apt).

    ruby_install_type: apt

By default, this role will install whatever version of ruby is available through your system's package manager (`apt`). You can install whatever version you like (including the latest release) by setting this to `ppa`, `rbenv`, `rvm`, or `source` and updating the `ruby_version`.

    ruby_version: 2.2.1

The version of ruby that will be installed (only used if `ruby_install_type` is anything other than `apt`).

    ruby_ppa_packages:
      - "ruby{{ ruby_version | truncate(3,True,'',0) }}"
      - "ruby{{ ruby_version | truncate(3,True,'',0) }}-dev"
      - ruby-switch

Array of ruby apt packages to install when installing via the [Brightbox PPA](https://www.brightbox.com/docs/ruby/ubuntu/).

    ruby_rbenv_profile: "/home/{{ ruby_user }}/.{{ 'zshrc_local' if ansible_user_shell == '/bin/zsh' else 'bashrc' }}"

Path to ruby rbenv file when installing via [Rbenv](https://github.com/rbenv/rbenv).

    ruby_rvm_dependencies:
      - libgdbm-dev
      - libncurses5-dev
      - automake
      - libtool
      - bison
      - libffi-dev

Dependency apt packages to install when installing Ruby via [Ruby Version Manager](https://rvm.io/).

    ruby_install_bundler: true

Whether this role should install [Bundler](http://bundler.io/).

    ruby_gems: []

A list of Ruby gems to install (just the name of the gem to be installed).

## Example Playbook

To run the role, include it as follows:

    - hosts: all
      roles:
         - { role: polymimetic.ruby, x: 42 }

## Credits

This role takes inspiration from the following Ansible roles:

- [geerlingguy.ruby](https://github.com/geerlingguy/ansible-role-ruby)

## License

This software package is licensed under the [MIT License](https://opensource.org/licenses/MIT). See the [LICENSE](./LICENSE) file for details.

## Author Information

This role was created in 2017 by [Polymimetic](https://github.com/polymimetic).

* ansible-role-ruby generated using [ansible-role-skeleton](https://github.com/polymimetic/ansible-role-skeleton)