# CloudEOS helm chart and operator for Kubernetes

This is a repo that is a step by step installation for a Helm chart using this github repo as a helm repo as well as converting that helm chart into a Kubernetes operator.

The helm chart can be used for any Kubernetes deployments.
The Kubernetes operator once certified can be used for any Kubernetes or Openshift deployment. 

It is assume that this install would be done on a client that has the [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) binary and (helm v3)[https://helm.sh/docs/intro/install/] binary installed as well.

## What is helm?

Helm is a scalable package manager for Kubernetes.  Helm uses what are called charts to install specific portions of kubernets(daemonsets, services, etc) to allow customizations of different Kubernetes parameters.  For example, a application running in a Kubernetes cluster may need some smaller tweeks like more resources or ingress into a specific url.  This would all be edited via a helm chart then deployed.  Helm will use the kubeconfig information to decide which Kubernetes cluster to deploy into. 

## What is a Kubernetes operator 

Kubernetes Operators simplify the management of Kubernetes applications.  Kubernetes operators aim to capture the key aim of human operation hence the name operator and apply those functions in a automated service and also so the deployments of Kuberneteds applications are a lot easier.  For example, a operator may watch a specific resource.  When a relevant event happens on the resource a condition is met and triggered on the operator. 

### How to create a local helm chart 
`helm package .`

### cloudeos-0.0.0.1.tgz will be created.

#### This will create a helm chart based off of everything within the current repo.  If need be make changes within the runnins-config.txt before running helm, package .  Also, if there are any needed changes make them with the values.yaml or Charts.yaml.

### To apply the the helm chart to a local kubernetes cluster
`helm install cloudeos-0.0.1.tgz --namespace kube-system --generate-name`

#### output

`NAME: cloudeos-0-1594668944`
`LAST DEPLOYED: Mon Jul 13 19:35:47 2020`
`NAMESPACE: kube-system`
`STATUS: deployed`
`REVISION: 1`
`TEST SUITE: None`

#### List the actual deployments
`helm ls --all-namespaces`

`NAME                   	NAMESPACE  	REVISION	UPDATED                                	STATUS`	`CHART           	APP VERSION`
`cloudeos-0-1594668944  	kube-system	1       	2020-07-13 19:35:47.509251293 +0000 UTC	deployed`

## To pull the helm chart from this repo 
#### Add the arista-cloudeos repo 
`helm repo add arista-cloudeos 'https://raw.githubusercontent.com/aristanetworks/cloudeos-k8s/helm-operator/master'`

#### Check the repo 
`helm repo ls`

`root@k8smaster:/opt/helmtesting/cloudeos# helm repo ls`
`NAME     	URL`
`arista-cloudeos  https://raw.githubusercontent.com/aristanetworks/cloudeos-k8s/helm-operator/master`

#### Install the helm chart

`helm install cloudeos arista-cloudeos/cloudeos`

## Convert from a Helmchart to a operator

`operator-sdk new cloudeos-operator --type=helm --helm-chart arista-cloudeos/cloudeos`

## Optional uninstall 

`helm uninstall cloudeos -n kube-system`



