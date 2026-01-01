
KinD
=========

Ansible role to quickly create a KinD on remote host for development and learning purposes.

Role Variables
--------------

Following variables needed for creating KinD keep in mind you can change the dafault values:
```
  - docker:
        group: "docker"
  - KinD:
        version: "v0.31.0"
        name: "test-kind"
        config_location: "/etc/kind_cluster.yml"
        config: |
            kind: Cluster
            apiVersion: kind.x-k8s.io/v1alpha4
            nodes:
                - role: control-plane
                - role: worker
```
Quick Start
----------------

you need to create 4 files to run this role properly.
 - requirements.yml

>      roles:
>        - name: kind
>          src: https://github.com/NavFar/KinD-ansible
>          version: main

 - Ansible.cfg
>   	 [defaults] 	 
>        interpreter_python=auto_silent
>        host_key_checking = False

 - playbook.yml

> 	  - hosts: all
>         become: true
>         roles:
>            - role: kind

 - inventory.yml

>      all:    hosts:
>       node1:
>         ansible_host: <YOUR REMOTE SERVER IP ADDRESS>
>         ansible_user: <YOUR REMOTE SERVER USER>

now you can install the role with following command
```
ansible-galaxy role install -r requirements.yml
```
then you can run your playbook with following command:
```
ansible-playbook  -i inventory.yml  playbook.yml
```

License
-------
MIT

Author Information
------------------
[Navid Farahmand](https://github.com/navfar)
