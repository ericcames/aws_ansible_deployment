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
vpc_name: aap_containerized_deployment
user_name: mickey.mouse
subnet_name: "{{ vpc_name }}_Subnet"
image: ami-06127bea7af8a9ad8
count: 1
region: us-west-1
assign_public_ip: true
alwaysup: false
instance_type: m5.xlarge
ec2_security_group_name: "{{ vpc_name }}_SECGRP"
ec2_ansible_group: "{{ user_name }}"
my_email_address: "{{ user_name }}@redhat.com"
my_ssh_key: my-ssh-key
ansible_python_interpreter: /usr/bin/python3
key_purpose: hello-world
key_name: mickeys-key
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