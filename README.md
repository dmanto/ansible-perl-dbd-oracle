# Ansible Role: install DBD::Oracle perl module

[![Build Status](https://travis-ci.org/dmanto/ansible-perl-dbd-oracle.svg?branch=master)](https://travis-ci.org/dmanto/ansible-perl-dbd-oracle)

Installs Perl DBD::Oracle module for RedHat/CentOS and Debian/Ubuntu linux servers.

## Requirements

You need to accept the licence agreement and download the proper files for your platform from the
oracle site:

http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html

you need the rpm files, (basic, devel & sqlplus), copied to the files/oralce directory. Please
assure that no other (probably older) files are in that directory (remove them if necessary).
There may be some files already on that directory because they are needed to test the role, but you do not have a licence to use them, so please remove them before running the role.

Tested platform are only Centos (6/7), Ubuntu (12.04, 14.04 and 16.04) and Fedora 24, all of them x86_64 versions. Special care was taken to avoid any other dependences that the mentioned here. For instance, some linux platforms do not have a standard 'find' command (i.e. Fedora 24), so in order to find oracle's home and lib directories it uses a perl oneliner, using File::Find core module which should be there because plenv and a decent new version of perl are already required.

Please open an issue to let me know if you are interested on this role running on other linux platforms.

## Role Variables

* app_user

default is "vagrant"

username of application user

## Dependencies

plenv and cpanm installed and available to the application user

## Example Playbook (creates user vicente, dir /home/vicente if it does not exist, with local perl 5.24.1 and then installs DBD::Oracle for the same user)

    - hosts: servers
      roles:
        - { role: dmanto.plenv-and-carton, app_user: "vicente", plenv_local: "5.24.1"}
        - { role: dmanto.perl-dbd-oracle, app_user: "vicente"}


## License

MIT / BSD

## Author Information

This role (specially testing aproach) was mainly inspired by ansible-role-java role written by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).

Author: Daniel Mantovani 2017
