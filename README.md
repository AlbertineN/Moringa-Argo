# Moringa Argo Playground
Learning at Moringa

## Prerequisites

1. Minikube
2. Git
3. Docker Hub account
4. Docker engine
### Commands

1. Start minikube

        minikube start
- Check minikube status

        minikube status
    It should be running

2. Make directory called Moringa, change into the directory and clone the repo provided:

        mkdir Moringa && cd Moringa && git clone https://github.com/CharlesGM/Moringa-Argo.git

3. Create argocd namespace and Install argo-cd 

        kubectl create namespace argocd
        kubectl -n argocd create -f argo.yaml

Wait for the pods to all be in running state. Run the command below to follow:

        kubectl get pods --watch -n argocd

4. Obtain argocd admin login password:

        kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

5. Port-forward your argocd server so that you can access it from your browser:

        Kubectl -n argocd get pods
        kubectl -n argocd port-forward argocd-server-xxxxxxxx 8080
