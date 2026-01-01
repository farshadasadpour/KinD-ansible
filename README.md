KinD
=========

Ansible role to quickly create a KinD on remote host for development and learning purposes.

Requirements
------------

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

Example Playbook
----------------
```
    - hosts: all
      become: true
      roles:
        - role: kind
          vars:
              KinD.name: "example-kind"
```

License
-------
MIT

Author Information
------------------
[Navid Farahmand](https://github.com/navfar)
