# CICD Deploymet to Kubernetes using Ansible
The purpose of this repository is to demonstrate how to deploy an app/service to Kubernetes using Ansible which can easily be run locally by a developer or a CI/CD platform such as Jenkins with little modification of the actual deployment code.  This ensures that what we develop locally on mimics how we deploy and run on production.  

First and formost, this is meant to be boilerplate code; Just enough to get you started if you will.  Its best if you cloned this into your existing app code repository with something like `git clone https://github.com/nickmaccarthy/ansible-kubernetes-deployment-sample.git kubernetes && rm -rf kubernetes/.git`. Please see the `Files` section below for documentation on what each file represents and does.

Here we run an Ansible playbook which creates a template file on the host where `kubectl` runs from, which we then run a `kubectl apply` which is what actually deploys to Kubernetes.  Since we are utilizing Ansible here we can utilize all that Ansible has to offer if we need to make deployments to Kubernetes more streamlined and efficient.

By default, our `kube.deployment.yml` is a basic [NodePort](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport) deployment in Kubernetes.  This helps emulate how many developers might develop against a `docker-compose` or with just a `docker run`.  This tempalte file can and should be modified to meet your needs for your specific app or service.  Remember this is just sample code, meant to just you going.  All modifications can then live your in app codes SCM going forward after you have cloned this in there. 

## Files
* `kube.deployment.playbook.yml` - The main deployment playbook used to deploy to kubernetes

* `kube-vars.yml` - variables that determine our service specific items, like ports, container image, tag, etc within the kubernetes template or application/deployment.  These can change and could even be made for different envrionments and each item within this could be overriden by passing along the `--extra-vars` flag when running `ansbile-playbook`.

* `templates/kube_deployment.yml` - This is a base template used to create a basic kubernetes deployment and pod.  This can easily be modified to meet your needs for your service 

## Usage 
1. Clone this repo into your application code repository
    * `git clone https://github.com/nickmaccarthy/ansible-kubernetes-deployment-sample.git kubernetes && rm -rf kubernetes/.git`
2. Modify the `kube-vars.yml` file to meet your needs 
3. Deploy your your kubernetes cluster 
    * `ansible-playbook kubernetes/kube.deployment.playbook.yml`

Note: If you wanted to backout the deployment running in Kubernetes, simply run this command: `ansible-playbook kubernetes/kube.deployment.playbook.yml --extra-vars '{deployment_enabled: false}'`

## Protip's
You can automate most of this with a Makefile.  Check out this Repo for more information

## Examples
Check out this repo for how this might look for an application code/deployment for more information.  I built a sample python Flask application that uses this repo for deployment a local K8S cluster. Check out - [k8s-flask-app-sample](https://github.com/nickmaccarthy/k8s-flask-app-sample)