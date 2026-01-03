
KinD
=========

Ansible role to quickly create a KinD (Kubernetes in Docker) cluster on a remote host for development and learning purposes.

## Features

- Installs Docker and required dependencies
- Downloads and installs kubectl and KinD binaries
- Configures bash autocompletion for kubectl
- Creates a Kubernetes cluster using KinD
- Copies kubeconfig to the user's home directory

## Prerequisites

- Ansible 2.2+
- SSH access to remote hosts
- `sshpass` installed (for password authentication): `sudo apt-get install sshpass`

## Role Variables

The following variables can be customized in `roles/kind/vars/main.yml`:

```yaml
docker:
  group: "docker"           # Docker group name

KinD:
  version: "v0.31.0"        # KinD version
  name: "test-kind"         # Cluster name
  config_location: "/etc/kind_cluster.yml"  # Config file path
  config: |                 # KinD cluster configuration
    kind: Cluster
    apiVersion: kind.x-k8s.io/v1alpha4
    nodes:
      - role: control-plane
      - role: worker
```

## Quick Start

### 1. Update inventory.yml

Edit `inventory.yml` with your remote server details:

```yaml
kind:
  hosts:
    node1:
      ansible_host: <YOUR_REMOTE_SERVER_IP>
      ansible_user: <YOUR_REMOTE_SERVER_USER>
```

### 2. Run the Playbook

Execute the playbook with password authentication:

```bash
ansible-playbook -i inventory.yml playbook.yml -k
```

The `-k` flag prompts for SSH password.

Alternatively, you can use SSH key authentication (no `-k` flag needed if keys are configured).

### 3. Verify Installation

After successful execution, SSH into the remote host and verify:

```bash
ssh <user>@<host>
kind get clusters
kubectl get nodes
```

## Project Structure

```
.
├── roles/kind/              # KinD role (self-contained)
│   ├── tasks/              # Role tasks
│   ├── defaults/           # Default variables
│   ├── vars/               # Role variables
│   ├── handlers/           # Handlers
│   └── meta/               # Role metadata
├── playbook.yml            # Main playbook
├── inventory.yml           # Inventory file
├── Ansible.cfg             # Ansible configuration
└── README.md              # This file
```

## License
MIT

## Author Information
[Navid Farahmand](https://github.com/navfar)
