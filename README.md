# argocd

Based off of https://argo-cd.readthedocs.io/en/stable/getting_started/

## Prerequisites 
* Minikube is running.
    * `minikube start`

## Deploying using Helm
You can deploy this project 2 different ways.

### Deploying directly from the inside the project
1. Deploy the Helm chart.
    * `helm install argocd argocd`

### Packaging the project and unstalling the tar file
1. We need to be outside the repo before we run these commands.
    * `cd ..`
2. Package the Helm chart.
    * `helm package argocd`
3. Deploy the Helm chart.
    * `helm install argocd argocd`

## Deploying using kubectl

### Install argocd into Minikube
1. Create the argocd namespace.
    * `kubectl apply -f templates/namespace.yaml`
2. Deploy argocd into the namespace.
    *`kubectl apply -n argocd -f templates/argo-install.yaml`

### Expose the argocd UI
`kubectl -n argocd port-forward svc/argocd-server 8080:443`

### Get the init log pwd for UI login
`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`

### Create An Application From A Git Repository


### Sync (Deploy) The Application

## Checking Deploy Status
`kubectl -n argocd get all`

## Deploying nginx-dummy-app using argocd
I've put together a small dummy Helm project called using nginx and we can use argocd to deploy it.
https://github.com/conorjduggan/nginx-dummy-app

### Creating the argocd app
1. After logging in, click the `+ New App` button.
2. Fill out the App config with the below values.
    * Application Name: `nginx-dummy-app`.
    * Project: `default`.
    * Sync Policy: `Manual`.
    * Repository URL: `https://github.com/conorjduggan/nginx-dummy-app.git`.
    * Revision: `HEAD`.
    * Path: `.`.
    * Cluster: `https://kubernetes.default.svc`.
    * Namespace: `default`.
3. Click `Create`.
4. You will now see your app in the argocd UI. Click into it.
5. Click `Sync` and argocd will deploy nginx-dummy-app. 