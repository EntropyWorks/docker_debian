~~docker_ubuntu~~ docker_debian
========

forked from angstwad/docker.ubuntu to run only on Debian. This is a tempory thing and eventually this will vanish.

**Example Play**:
```
---
- name: Run docker_debian
  hosts: docker
  roles:
    - docker_debian
```

Overriding the role's default variables is also pretty straightforward:
```
- name: Install Docker on Rax Server
  hosts: all
  roles:
    - role: docker_debian
      ssh_port: 2222
      kernel_pkg_state: present
```


Requirements
------------

Requires python-pycurl for apt modules.

Role Variables
--------------

These are the defaults, which can be set to present to prevent a reboot if the latest linux-image-extra, cgroup-lite packages are already installed.
The following role variables are defined:

```
---
# lxc-docker is the default
docker_pkg_name: docker-engine
# docker_pkg_name: docker.io
# Important if running Ubuntu 12.04-13.10 and ssh on a non-standard port
ssh_port: 22
# Place to get apt repository key
apt_key_url: http://get.docker.io/gpg
# apt repository key signature
apt_key_sig: A88D21E9
# Name of the apt repository for docker
apt_repository: deb https://get.docker.com/ubuntu docker main
# The following help expose a docker port or to add additional options when
# running docker daemon.  The default is to not use any special options.
#docker_opts: >
#  -H unix://
#  -H tcp://0.0.0.0:2375
#  --log-level=debug
docker_opts: ""
# List of users to be added to 'docker' system group (disabled by default)
# SECURITY WARNING:
# Be aware that granted users can easily get full root access on the docker host system!
docker_group_members: []
# Versions for the python packages that are installed
pip_version_pip: latest
pip_version_setuptools: latest
pip_version_docker_py: latest
pip_version_docker_compose: latest

# If this variable is set to true kernel updates and host restarts are permitted.
# Warning: Use with caution in production environments.
kernel_update_and_reboot_permitted: no
# Set to 'yes' or 'true' to enable updates (sets 'latest' in apt module)
update_docker_package: no
# Change these to 'present' if you're running Ubuntu 12.04-13.10 and are fine with less-than-latest packages
kernel_pkg_state: latest
cgroup_lite_pkg_state: latest
# Force an install of the kernel extras, in case you're suffering from some issue related to the
# static binary provided by upstream Docker.  For example, see this GitHub Issue in Docker:
# https://github.com/docker/docker/issues/12750
# Warning: Installing kernel extras is potentially interruptive/destructive and will install backported
# kernel if running 12.04.
install_kernel_extras: false
# Install Xorg packages for backported kernels.  This is usually unnecessary except for environments
# where an X/Unit desktop is actively being used. If you're not using an X/Unity on 12.04, you
# won't need to enable this.
install_xorg_pkgs: false

```

Dependencies
------------

None.

Requires `ansible-playbook` to be in the path.

License
-------

Apache v2.0
