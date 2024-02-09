# Overview
An Ansible playbook that installs Kubernetes.

A guide for using this repo to spin up a Kubernetes cluster is available at [Installing your Kubernetes homelab cluster in minutes with Ansible](https://perdue.dev/installing-your-kubernetes-homelab-cluster-in-minutes-with-ansible/)


# Credits

Code examples originally adapted from https://perdue.dev/installing-your-kubernetes-homelab-cluster-in-minutes-with-ansible/


# Features
- containerd
- calico for pod networking


# Installation

1. Update inventory/dev with IPs for each master/slave nodes

2. Install a Python virtual envrionment:

```python
python3 -m venv ./venv
```

3. Install `ansible` within the venv

`python3 -m pip install ansible`

4. Run `keyscan.py`

Output will look like:

```bash
['homelabvm1', 'homelabvm2', 'homelabvm3', 'homelabvm4']
# homelabvm1:22 SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.6
# homelabvm2:22 SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.6
# homelabvm4:22 SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.6
# homelabvm3:22 SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.6
```


5. Run `ansible -i inventory/dev all -m ping --user ansible`

Output will look like:

```bash
homelabvm1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
homelabvm2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
homelabvm3 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
homelabvm4 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```


6. Run `ansible-playbook -i inventory/dev playbooks/k8s_all.yaml --user ansible`
