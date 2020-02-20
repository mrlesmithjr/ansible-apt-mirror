# ansible-apt-mirror

Ansible role to setup an APT mirror

> NOTE: Installs and configures apt-mirror (Local APT Repository).
> Also configures clients if extra-var passed.

## Build Status

### GitHub Actions

![Molecule Test](https://github.com/mrlesmithjr/ansible-apt-mirror/workflows/Molecule%20Test/badge.svg)

### Travis CI

[![Build Status](https://travis-ci.org/mrlesmithjr/ansible-apt-mirror.svg?branch=master)](https://travis-ci.org/mrlesmithjr/ansible-apt-mirror)

## Requirements

Lot's of disk space required for repos...At the time of putting this together Ubuntu Trusty w/defaults in this role requires 139GB+

For any required Ansible roles, review:
[requirements.yml](requirements.yml)

## Role Variables

[defaults/main.yml](defaults/main.yml)

## Dependencies

## Example Playbook

[playbook.yml](playbook.yml)

## License

MIT

## Author Information

Larry Smith Jr.

- [@mrlesmithjr](https://twitter.com/mrlesmithjr)
- [mrlesmithjr@gmail.com](mailto:mrlesmithjr@gmail.com)
- [http://everythingshouldbevirtual.com](http://everythingshouldbevirtual.com)

> NOTE: Repo has been created/updated using [https://github.com/mrlesmithjr/cookiecutter-ansible-role](https://github.com/mrlesmithjr/cookiecutter-ansible-role) as a template.
