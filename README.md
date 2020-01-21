** cert-manager installation on kubernetes , based on : https://cert-manager.io/docs/installation/kubernetes/

1. create namespace:
```
kubectl create namespace cert-manager
```
2. We can now go ahead and install cert-manager. All resources (the CustomResourceDefinitions, cert-manager, and the webhook component) are included in a single YAML manifest file:

```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.12.0/cert-manager.yaml
```
( you can skip the "--validate=false" flag, if you are using kubernetes v1.15 or higher)

Note: When running on GKE (Google Kubernetes Engine), you may encounter a ‘permission denied’ error when creating some of these resources. This is a nuance of the way GKE handles RBAC and IAM permissions, and as such you should ‘elevate’ your own privileges to that of a ‘cluster-admin’ before running the above command. If you have already run the above command, you should run them again after elevating your permissions:

```
kubectl create clusterrolebinding cluster-admin-binding \
  --clusterrole=cluster-admin \
  --user=$(gcloud config get-value core/account)
```
