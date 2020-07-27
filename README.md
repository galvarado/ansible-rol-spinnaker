# ansible-rol-spinnaker

Ansible role to install a production ready Spinnaker.

This deployment is based on:
- Local environment (local debian installation)
- Kubernetes as a cloud provider 
- Google Cloud Storage as external storage provider
- Google Container Registry as docker registry

Read more at:
- https://spinnaker.io/setup/install/environment/
- https://spinnaker.io/setup/install/providers/kubernetes-v2/ 
- https://spinnaker.io/setup/install/storage/
- https://spinnaker.io/setup/install/providers/docker-registry/

## How to use 

### Requirements

- A VM based on Ubuntu 16.04 to install spinnaker (at least 4 cores and 16GB of RAM)
- In order to connect to Spinnaker UI VM must have ports 22,9000, 8084 enabled.
- A running kubernetes cluster
- You must have gcloud installed (some scripts use it)
- Create a kubernetes service account for spinnaker (instructions provided above)
- Be able to create a gcloud service account for spinnaker to manage gcs (instructions provided above)
- Be able to create a gcloud service account for spinnaker to manage gcr (instructions provided above)

### 1. Add to your ansible hosts file an entry for spinnaker:

```
[spinnaker]
x.x.x.x
```

### 2. Create A kubernetes namespace, a service account and grant a role for spinnaker

Execute the script located at:

```
scripts/create_spinnaker_k8s_service_account.sh
```

It will create a spinnaker service account in the target kubernetes.

Execute the script located at:

```
sripts/create_kubeconfig_file.sh
```

Pass the following arg and save the output to a file called kubeconfig as follows:
```
.create_kubeconfig_file.sh spinnaker-service-account > kubeconfig
```


It will create a kubeconfig file that will be transfered to the spinnaker server. Whith that file, spinnaker will manage the k8s cluster.

Copy the kubeconfig file generated in the following path:

```
playbooks/templates/kubeconfig
```


### 3. Create a google service account to spinnaker be able to manage GCS:

Execute the script located at:
```
scripts/create_spinnaker_gcloud_gcs_service_account.sh
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

You can check your service accounts at: https://console.cloud.google.com/apis/credentials

### 4. Create a google service account to spinnaker be able to manage images at GCR:

In order to spinnaker be able to pull container images at Google Container Registry, Execute the script located at:
```
scripts/create_spinnaker_gcloud_gcr_service_account.sh
```

The script will crete the service account named spinnaker-grs-account. 

You must copy the json file that contains the auth information of the service account. It is generated usually under 

```

/home/$USER/.gcp/gcr-account.json

```

Copy it in the following path:

```
playbooks/templates/gcr-account.json
```

You can check your service accounts at: https://console.cloud.google.com/apis/credentials


### 5. playbook variables

```
PENDING
```
### 6. Execute the playbook

```
ansible-playbook install_spinnaker.yml 
```

So, you are ready to do Continuos Deployment in your k8s =) 

When the playbook complete successufuly, go to http://[spinnaker_domain]:9000

