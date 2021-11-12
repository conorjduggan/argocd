# argocd-test

Based off of https://argo-cd.readthedocs.io/en/stable/getting_started/

## Prerequisites 
* Minikube is running.
    * `minikube start`

## Install argocd into Minikube
1. Create the argocd namespace.
    * `k apply -f templates/namespace.yaml`
2. Deploy argocd into the namespace.
    *`k apply -n argocd -f templates/argo-install.yaml`

## Expose the argocd UI
`kubectl -n argocd port-forward svc/argocd-server 8080:443`

## Get the init log pwd for UI login
`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`

## Create An Application From A Git Repository


## Sync (Deploy) The Application


