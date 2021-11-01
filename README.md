# Ansible Role: zoom
[![Role gotmax23.zoom][badge-role]][link-galaxy]
[![Github Repo][badge-github-repo]][link-github-repo]
[![SourceHut Repo][badge-srht-repo]][link-srht-repo]
[![MIT Licensed][badge-license]][link-license]
[![Github Open Issues][badge-github-issues]][link-github-issues]
[![Github Open PRs][badge-github-prs]][link-github-prs]
[![Role Version][badge-version]][link-version]
[![Commits since last version][badge-commits-since]][link-version]
[![Galaxy Role Quality][badge-quality]][link-galaxy]
[![Galaxy Role Downloads][badge-downloads]][link-galaxy]
[![Github Actions Molecule workflow status][badge-molecule-workflow]][link-molecule-workflow]
[![Github Actions Galaxy workflow status][badge-galaxy-workflow]][link-galaxy-workflow]

Ansible role that installs the Zoom client on Linux.

## Beta Warning
**This role is currently in beta and is not intended for production use. Breaking changes may occur between releases, so please make sure to read the release notes.**
## Requirements

This role depends on certain collections that are not included in ansible-core.


To install this role's requirements, create a `requirements.yml` file with the following contents:

``` yaml
# SPDX-FileCopyrightText: 2021 Maxwell G (@gotmax23)
# SPDX-License-Identifier: CC0-1.0
---
collections:
  - name: community.general

```

Then, if you are using ansible-base/ansible-core 2.10 or later, run this command.

``` shell
ansible-galaxy install -r requirements.yml
```


If you are still using Ansible 2.9, run this command, instead.

``` shell
ansible-galaxy collection install -r requirements.yml
```

## Role Variables

Here are this role's variables and their default values, as set in [`defaults/main.yml`][link-defaults]. If you'd like, you may change them to customize this role's behavior.

``` yaml
# SPDX-FileCopyrightText: 2021 Maxwell G (@gotmax23)
# SPDX-License-Identifier: CC0-1.0
---
# Options:
# - `present` ensures that Zoom is installed.
# - `absent` ensures that Zoom is not installed.
zoom_state: present

# This option dictates whether to check zoom's rpm key fingerprint.
zoom_check_rpm_key: true

# This variable dictates where this role will download the Zoom pacman pkg archive.
# This only applies to Archlinux.
zoom_pacman_pkg_download_dir: /opt

```

## Example Playbook
``` yaml
# SPDX-FileCopyrightText: 2021 Maxwell G (@gotmax23)
# SPDX-License-Identifier: CC0-1.0
---
- name: Install zoom
  hosts: all
  become: true

  tasks:
    - name: Update apt cache
      when: ansible_pkg_mgr == "apt"
      ansible.builtin.apt:
        update_cache: true
        cache_valid_time: 3600

    - name: Install zoom
      ansible.builtin.include_role:
        name: "gotmax23.zoom"

```

## Compatibility
This role is tested using the latest version of ansible-core and the latest version of the collections from Ansible Galaxy. This is the only version of Ansible that this role officially supports. Best effort support is provided for other versions.

This role is compatible with the following distros:

|distro|versions|
|------|--------|
|Archlinux|any|
|Debian|buster, bullseye, bookworm|
|EL|7, 8|
|Fedora|34, 35, 36|
|opensuse|15.2, 15.3, tumbleweed|
|Ubuntu|bionic, focal|

## License
[MIT][link-license]

## Author
Maxwell G (@gotmax23)

[badge-role]: https://img.shields.io/ansible/role/56753.svg?logo=ansible
[link-galaxy]: https://galaxy.ansible.com/gotmax23/zoom
[badge-github-repo]: https://img.shields.io/static/v1?label=GitHub&message=repo&color=blue&logo=github
[link-github-repo]: https://github.com/gotmax23/ansible-role-zoom
[badge-srht-repo]: https://img.shields.io/static/v1?label=SourceHut&message=repo&color=blue&logo=data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+CjxzdmcKICAgdmlld0JveD0iMCAwIDUxMiA1MTIiCiAgIHZlcnNpb249IjEuMSIKICAgaWQ9InN2ZzUxIgogICBzb2RpcG9kaTpkb2NuYW1lPSJzb3VyY2VodXQtd2hpdGUuc3ZnIgogICBpbmtzY2FwZTp2ZXJzaW9uPSIxLjEgKGM2OGUyMmMzODcsIDIwMjEtMDUtMjMpIgogICB4bWxuczppbmtzY2FwZT0iaHR0cDovL3d3dy5pbmtzY2FwZS5vcmcvbmFtZXNwYWNlcy9pbmtzY2FwZSIKICAgeG1sbnM6c29kaXBvZGk9Imh0dHA6Ly9zb2RpcG9kaS5zb3VyY2Vmb3JnZS5uZXQvRFREL3NvZGlwb2RpLTAuZHRkIgogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciCiAgIHhtbG5zOnN2Zz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogIDxkZWZzCiAgICAgaWQ9ImRlZnM1NSIgLz4KICA8c29kaXBvZGk6bmFtZWR2aWV3CiAgICAgaWQ9Im5hbWVkdmlldzUzIgogICAgIHBhZ2Vjb2xvcj0iIzUwNTA1MCIKICAgICBib3JkZXJjb2xvcj0iI2ZmZmZmZiIKICAgICBib3JkZXJvcGFjaXR5PSIxIgogICAgIGlua3NjYXBlOnBhZ2VzaGFkb3c9IjAiCiAgICAgaW5rc2NhcGU6cGFnZW9wYWNpdHk9IjAiCiAgICAgaW5rc2NhcGU6cGFnZWNoZWNrZXJib2FyZD0iMSIKICAgICBzaG93Z3JpZD0iZmFsc2UiCiAgICAgaW5rc2NhcGU6em9vbT0iMS42NTQyOTY5IgogICAgIGlua3NjYXBlOmN4PSIyNTYiCiAgICAgaW5rc2NhcGU6Y3k9IjI1NiIKICAgICBpbmtzY2FwZTp3aW5kb3ctd2lkdGg9IjE5MjAiCiAgICAgaW5rc2NhcGU6d2luZG93LWhlaWdodD0iMTA1OSIKICAgICBpbmtzY2FwZTp3aW5kb3cteD0iMCIKICAgICBpbmtzY2FwZTp3aW5kb3cteT0iMCIKICAgICBpbmtzY2FwZTp3aW5kb3ctbWF4aW1pemVkPSIxIgogICAgIGlua3NjYXBlOmN1cnJlbnQtbGF5ZXI9InN2ZzUxIiAvPgogIDxwYXRoCiAgICAgZD0iTTI1NiA4QzExOSA4IDggMTE5IDggMjU2czExMSAyNDggMjQ4IDI0OCAyNDgtMTExIDI0OC0yNDhTMzkzIDggMjU2IDh6bTAgNDQ4Yy0xMTAuNSAwLTIwMC04OS41LTIwMC0yMDBTMTQ1LjUgNTYgMjU2IDU2czIwMCA4OS41IDIwMCAyMDAtODkuNSAyMDAtMjAwIDIwMHoiCiAgICAgaWQ9InBhdGg0OSIKICAgICBzdHlsZT0iZmlsbDojZmZmZmZmIiAvPgo8L3N2Zz4K
[link-srht-repo]: https://git.sr.ht/~gotmax23/ansible-role-zoom
[badge-license]: https://img.shields.io/github/license/gotmax23/ansible-role-zoom.svg?logo=github
[link-license]: https://github.com/gotmax23/ansible-role-zoom/blob/main/LICENSE
[badge-github-issues]: https://img.shields.io/github/issues/gotmax23/ansible-role-zoom.svg?logo=github
[link-github-issues]: https://github.com/gotmax23/ansible-role-zoom/issues
[badge-github-prs]: https://img.shields.io/github/issues-pr/gotmax23/ansible-role-zoom.svg?logo=github
[link-github-prs]: https://github.com/gotmax23/ansible-role-zoom/pulls
[badge-version]: https://img.shields.io/github/release/gotmax23/ansible-role-zoom.svg?logo=github
[link-version]: https://github.com/gotmax23/ansible-role-zoom/releases/latest
[badge-commits-since]: https://img.shields.io/github/commits-since/gotmax23/ansible-role-zoom/latest.svg?logo=github
[badge-quality]: https://img.shields.io/ansible/quality/56753.svg?logo=ansible
[badge-downloads]: https://img.shields.io/ansible/role/d/56753.svg?logo=ansible
[badge-molecule-workflow]: https://github.com/gotmax23/ansible-role-zoom/actions/workflows/molecule.yml/badge.svg?branch=main
[link-molecule-workflow]: https://github.com/gotmax23/ansible-role-zoom/actions/workflows/molecule.yml
[badge-galaxy-workflow]: https://github.com/gotmax23/ansible-role-zoom/actions/workflows/galaxy.yml/badge.svg
[link-galaxy-workflow]: https://github.com/gotmax23/ansible-role-zoom/actions/workflows/galaxy.yml
[link-defaults]: https://github.com/gotmax23/ansible-role-zoom/blob/main/defaults/main.yml
