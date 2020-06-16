Ansible Role: GraalVM
=====================

Role to install the GraalVM CE.

**Important:** This ansible role is based on [GANTSIGN ansible-role-java](https://github.com/gantsign/ansible-role-java)

Requirements
------------

* Ansible >= 2.8

* Linux Distribution

    * Debian Family

        * Ubuntu

            * Focal (20.04)
            * Bionic (18.04)

    * Note: other versions are likely to work but have not been tested.

Role Variables
--------------

The following variables will change the behavior of this role (default values
are shown below):

```yaml
# specify the underlying java version
# 8 or 11
graalvm_java_version: '11'

# GraalVM version number
graalvm_version: '20.1.0'

# Base installation directory for any GraalVM distribution
graalvm_install_dir: '/opt/graalvm'

# Directory to store files downloaded for GraalVM installation on the remote box
graalvm_download_dir: "{{ x_ansible_download_dir | default(ansible_env.HOME + '/.ansible/tmp/downloads') }}"

# If this is the default installation, profile scripts will be written to set
# the GRAALVM_HOME environment variable
graalvm_is_default_installation: true

# If this graalvm bin director should be add to PATH environment variable
# Effect is only when this is also the default installation
graalvm_add_to_path: true

# Location GraalVM installations packages can be found on the local box
# local packages will be uses in preference to downloading new packages.
graalvm_local_archive_dir: '{{ playbook_dir }}/files'

# Wether to use installation packages in the local archive (if available)
graalvm_use_local_archive: true

# The SHA-256 for the GraalVM redistributable
graalvm_redis_sha256sum:

# location for GraalVM download (e.g. https://example.com/provisioning/files)
# specify only when NOT downloading from directly github
graalvm_redis_mirror: 

# File name for the GraalVM redistributable installation file
graalvm_redis_filename: "graalvm-ce-java{{ graalvm_java_version }}-linux-amd64-{{ graalvm_version }}.tar.gz"

# Name of the group of Ansible facts relating this GraalVM installation.
#
# Override if you want use this role more than once to install multiple versions
# of GraalVM.
#
# e.g. graalvm_fact_group_name: graalvm_19.3
# would change the GraalVM home fact to:
# ansible_local.graalvm_19.3.general.home
graalvm_fact_group_name: graalvm

# Timeout for GraalVM download response in seconds
graalvm_download_timeout_seconds: 600
```

Example Playbooks
-----------------

By default this role will install the latest GraalVM CE that has been tested and is known to work with this role:

```yaml
- hosts: servers
  roles:
    - role: arolfes.graalvm
```
