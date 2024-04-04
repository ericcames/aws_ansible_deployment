infrastructure
=========

This role will create the infrastructure we need at AWS.

Requirements
------------
```yaml
---
Amazon Web Console Account
Amazon Web Services Credential in Ansible Automation Platform
```
Role Variables
--------------
```yaml
---
# Infrastructure Defaults
infrastructure_region: us-west-1
infrastructure_tags: []

# Networking
infrastructure_vpc_cidr: 172.16.0.0/22
infrastructure_vpc_subnets:
  - name: controller
    cidr: 172.16.0.0/24
    az: us-west-1a
  - name: execution
    cidr: 172.16.1.0/24
    az: us-west-1a
  - name: hub
    cidr: 172.16.2.0/24
    az: us-west-1a
  - name: eda
    cidr: 172.16.3.0/24
    az: us-west-1a

# Compute
infrastructure_assign_public_ip: true
infrastructure_delete_on_termination: true
infrastructure_architecture: x86_64

infrastructure_ami_filter:
  architecture: "{{ infrastructure_architecture }}"
  owner-id: "309956199498"
  name: "RHEL-9.2.*_HVM-*"

infrastructure_volumes:
  - device_name: /dev/sda1
    ebs:
      volume_type: io1
      volume_size: 100
      iops: 1500
      delete_on_termination: true

infrastructure_cert_local_folder_path: /etc/ssl/
infrastructure_cert_domain_name: my.custom.domain

infrastructure_create_controller_lb: false
infrastructure_lb_scheme: internet-facing

infrastructure_controller_instances: 1
infrastructure_controller_shape: m5a.xlarge

infrastructure_execution_instances: 0
infrastructure_execution_shape: m5a.xlarge

infrastructure_hub_instances: 1
infrastructure_hub_shape: m5a.large

infrastructure_eda_instances: 0
infrastructure_eda_shape: m5a.xlarge

# Database
infrastructure_db_username: ansible
infrastructure_db_password: changeme

infrastructure_db_engine_version: "13.12"
infrastructure_db_allow_major_version_upgrade: false
infrastructure_db_auto_minor_version_upgrade: true
infrastructure_db_multi_az: false
infrastructure_db_storage_encrypted: true
infrastructure_db_db_instance_class: db.m5d.xlarge
infrastructure_db_storage_type: io1
infrastructure_db_storage_iops: 5000
infrastructure_db_allocated_storage: 100

# RHEL
infrastructure_aap_version: "2.4"
infrastructure_rhel_version: "9"
```
Dependencies
------------
```yaml
amazon.aws
```
Example Playbook
----------------
```yaml
---
- name: Create infrastructure
  hosts: localhost
  connection: local

  roles:

    - name: infrastructure
```
License
-------

https://spdx.org/licenses/GPL-3.0-only.html

Author Information
------------------
```yaml
Eric C Ames
```
ericcames@msn.com