# ansible-rol-spinnaker

Ansible roles to install a production ready Spinnaker.

This deployment is based on:
- Local environment (local debian installation)
- Kubernetes as a cloud provider
- Google Cloud Storage as external storage provider

Read more at:
- https://spinnaker.io/setup/install/environment/
- https://spinnaker.io/setup/install/providers/kubernetes-v2/ 
- https://spinnaker.io/setup/install/storage/


## How to use 

### Requirements

- A VM based on Ubuntu 16.04 to install spinnaker (at least 4 cores and 16GB of RAM)
- In order to connect to Spinnaker UI VM must have ports 22,9000, 8084 enabled.
- A running kubernetes cluster
- A valid kubeconfig file
- Be able to create a gcloud service account for spinnaker (instructions provided above)

### 1. Add to your ansible hosts file an entry for spinnaker:

```
[spinnaker]
x.x.x.x
```

### 2. Place your kubeconfig file:

Copy and paste a valid kubeconfig file in the following path:

```
playbooks/templates/kubeconfig
```

It will be used by kubectl to create a spinnaker service account in the target kubernetes.

### 3. Create a google service account to spinnaker be able to manage GCS:

Execute the script located at
```
scripts/create_spinnaker_gcloud_service_account.sh
```

You must be logged in with gcloud in the project is intended to use. The script will crete the service account named spinnaker-gcs-account. 

You must copy the json file that contains the auth information of the service account. It is generated usually under 

```

/home/$USER/.gcp/gcs-account.json

```

Copy it in the following path:

```
playbooks/templates/gcs-account.json
```

### 4. playbook variables

```
PENDING
```
### 5. Execute the playbook

```
ansible-playbook install_spinnaker.yml 
```

When the playbook complete successufl, go to http://[YOU_PUBLIC_IP_ADDRESS]:9000

So, you are ready to do Continuos Deployment in your k8s =) 
