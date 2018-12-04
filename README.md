# NodePort Deployment to Kubernetes with Ansible
The purpose of this repository is to demonstrate how to deploy an app/service to Kubernetes using Ansible.  

This runs an ansible playbook which created a template file which which in turn calls `kubectl` to deploy to kubernetes.  

## Files
* `kube.deployment.playbook.yml` - The main deployment playbook used to deploy to kubernetes

* `kube-vars.yml` - variables that determine our service specific items, like ports, container image, tag, etc within the kubernetes template or application/deployment.  These can change and could even be made for different envrionments and each item within this could be overriden by passing along the `--extra-vars` flag when running `ansbile-playbook`.

* `templates/kube_deployment.yml` - This is a base template used to create a basic kubernetes deployment and pod.  This can easily be modified to meet your needs for your service 

## Usage 
1. Clone this repo into your application code repository. 
2. Consider renaming the folder to something different, perhaps `kubernetes` 
3. Modify the `kube-vars.yml` file to meet your needs 
4. Deploy your your kubernetes cluster 
    * `ansible-playbook kubernetes/kube.deployment.playbook.yml`

Note: If you wanted to backout the deployment running in Kubernetes, simply run this command: `ansible-playbook kubernetes/kube.deployment.playbook.yml --extra-vars '{deployment_enabled: false}'`

## Protip's
You can automate most of this with a Makefile.  Check out this Repo for more information

## Examples
Check out this repo for how this might look for an application code/deployment for more information