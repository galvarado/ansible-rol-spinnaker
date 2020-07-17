# ansible-rol-spinnaker

Ansible roles to install a production ready Spinnaker.

This deployment is based on:
- local debian installation
- kubernetes as a cloud provider
- Google Cloud Storage as external storage provider

Read more at:

- https://spinnaker.io/setup/install/environment/
- https://spinnaker.io/setup/install/providers/kubernetes-v2/ 
- https://spinnaker.io/setup/install/storage/


## How to use 

### Requirements

- A VM based on Ubuntu 16.03 to install spinnaker
- A running kubernetes cluster
- A valid kubeconfig file

### 1. Add to your ansible hosts file an entry for spinnaker:

```
[spinnaker]
x.x.x.x
```

### 2. Place your kubeconfig file:

Copy and paste a valid kubeconfig file in the following path:

```
templates/kubeconfig
```

It will be used by kubectl to create a spinnaker service account the target kubernetes.

