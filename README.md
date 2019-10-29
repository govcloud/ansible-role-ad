# Ansible Role: Installs and configures Active Directory on Linux.

Travis status:   [![Build Status](https://travis-ci.org/KAMI911/ansible-role-linux-ad.svg?branch=master)](https://travis-ci.org/KAMI911/ansible-role-linux-ad)
Code Climate status: [![Code Climate](https://codeclimate.com/github/KAMI911/ansible-role-linux-ad/badges/gpa.svg)](https://codeclimate.com/github/KAMI911/ansible-role-linux-ad)
Test Coverage status: [![Test Coverage](https://codeclimate.com/github/KAMI911/ansible-role-linux-ad/badges/coverage.svg)](https://codeclimate.com/github/KAMI911/ansible-role-linux-ad/coverage)

## Table of Contents

1. [Requirements][Requirements]
2. [Installation][Installation]
3. [Role Variables][Role Variables]
4. [Dependencies][Dependencies]
5. [Example Playbook][Example Playbook]
6. [Licensing][Licensing]
7. [Author Information][Author Information]
8. [Support][Support]
9. [Contributing][Contributing]
10. [Donation][Donation]

## Requirements

None.

## Installation

    ansible-galaxy install kami911.linux-ad

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    linux_ad_authconfig_debug_mode: false

Use authconfig debug mode.

    linux_ad_authconfig_debug_level: 3

Set authconfig debug level.

    linux_ad_authconfig_domain: 'cloud.department.ca'

Set authconfig (FQDN) domain name.

    linux_ad_authconfig_realm:  'CLOUD.DEPARTMENT.CA'

Set authconfig realm name.

    linux_ad_authconfig_computer_ou: 'ou=computers,dc=cloud,dc=department,dc=ca'

Set the Active Directory path to computers organization unit.

    linux_ad_authconfig_windomain: 'EXAMPLECOM'

Set authconfig Windows domain name.

    linux_ad_authconfig_sssd_user: 'admin'

Specify an already existing domain user that has 'add computer to domain' rights.

    linux_ad_authconfig_sssd_pass: 'pass'

Specify the password of that domain user.

    linux_ad_authconfig_access_groups: []

An array/list of groups that have access to the host.

    linux_ad_authconfig_access_users: []

An array/list of users that have access to the host.

    linux_ad_ansible_distribution_major_version: '{{ ansible_lsb.major_release|int }}'

Specify the main version of your Linux OS if something gets wrong and the version is not available.

    linux_ad_ad_info_ad_server: 'dc1.department.ca'

    linux_ad_ad_info_ad_backup_server: 'dc2.department.ca'

Specify the primary and a backup Active Directory login server.

    linux_ad_rejoin: false

Try to rejoint to the Active Directory bia deleting /etc/krb5.keytab file. Default is false.

    linux_ad_home_dir: '/home/%d/%u'

Home directory of the user.
Additionally you can use these variables:
%u -login name
%U - UID number
%d - domain name
%f - fully qualified user name (user@domain))
%% - %.

    linux_ad_shell: '/bin/bash'

Shell to use for freshly created users.

    linux_ad_home_dir_base:
      - '/home/{{ linux_ad_authconfig_domain }}'

If you not using /home/%s as home directory, the script have to create all of required domains subdirectory (in this example case /home/cloud.department.ca/). Please list all possible domains here.

    linux_ad_home_dir_user: 'root'

The user of the newly created subhome directory.

    linux_ad_home_dir_group: 'root'

The group of the newly created subhome directory.

    linux_ad_home_dir_mode: 755

The mode of the newly created subhome directory.

    linux_ad_sudoers_d:
    - file: linux_ad
        host: ALL
        runas: ALL
        ugid: '%Enterprise\ Admins'
        nopasswd: true
        commands:
        - 'ALL'

Create sudoers file with these parameters. The file is filename of the created file in sudoers.d.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - linux-ad

## Licensing

The lactransformer application and documantations are licensed under the terms of
the MIT / BSD, you will find a copy of this license in the
[LICENSE](LICENSE) file included in the source package.

## Author Information

This role was created in 2019 by Kálmán Szalai - KAMI based on work of William Hearn (https://github.com/govcloud/ansible-role-ad)

## Support

If you have any question, do not hesitate and drop me a line.
If you found a bug, or have a feature request, you can [fill an issue](https://github.com/KAMI911/ansible-role-linux-ad/issues).

## Contributing

There are many ways to contribute to ansible-role-linux-ad -- whether it be sending patches,
testing, reporting bugs, or reviewing and updating the documentation. Every
contribution is appreciated!

Please continue reading in the [contributing chapter](CONTRIBUTING.md).

### Fork me on Github

https://github.com/KAMI911/ansible-role-linux-ad

Add a new remote `upstream` with this repository as value.

```
git remote add upstream https://github.com/KAMI911/ansible-role-linux-ad.git
```

You can pull updates to your fork's master branch:

```
git fetch --all
git pull upstream HEAD
```

## Donation

If you find this useful, please consider a donation:

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=RLQZ58B26XSLA)


<!-- TOC URLs -->
[Requirements]: #requirements
[Installation]: #installation
[Role Variables]: #role_variables
[Dependencies]: #dependencies
[Example Playbook]: #example_playbook
[Licensing]: #licensing
[Author Information]: #author_information
[Support]: #support
[Contributing]: #contributing
[Donation]: #donation
