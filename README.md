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

   Alternatively, you can set up a LoadBalancer service to get an external IP through which you can access your site.

   First, get your  minikube ip by running the command

           minikube ip
   Navigate to the K8s directory

           cd K8s
   Create the service in the frontend namespace

           kubectl create -f service.yaml -n frontend
   patch your node ip as a LoadBalancer to the service created

           kubectl patch svc moringa-web-page-service -n frontend -p '{"spec": {"type": "LoadBalancer", "externalIPs":["192.168.49.2"]}}' #replace "192.168.49.2" with your minikube ip
   Use you minikube ip to access the website

           http://192.168.49.2/

         
