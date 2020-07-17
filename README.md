# ansible-rol-spinnaker

Ansible roles to install a production ready Spinnaker based on local debian installation and using kubernetes as a cloud provider.

Read more about the spinnaker environment at: https://spinnaker.io/setup/install/environment/

Read more abunt spinnaker kubernetes cloud provider at: https://spinnaker.io/setup/install/providers/kubernetes-v2/ 


## How to use 

### Requirements

- A VM based on Ubuntu 16.03 to install spinnaker
- A running kubernetes cluster
- A valid kubeconfig file

### 1. Add to your ansible hosts file an entry for spinnaker:

´´´
[spinnaker]
x.x.x.x
´´´

### 2. Place your kubeconfig file:

Copy and paste a valid kubeconfig file in the following path: templates/kubeconfig:


