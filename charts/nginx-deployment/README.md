# NGINX Deployment using helm

## Prerequisites
- Kubernetes cluster is set up and configured.
- Helm is installed and initialized on the Kubernetes cluster.
- Access to the cluster with sufficient privileges to create and manage resources.

## Step 1: Clone the Helm Chart Repository
Clone the Helm chart repository that contains the Nginx chart:
-  git clone repository-url
-  cd chart-directory

## Step 2: Update the Helm Chart Values
Update the values in the Helm chart to configure Nginx and the associated resources.
- vi values.yaml

In values.yaml file you can update values like no. of replicas you want, Image name, service type which you want to use and also on which port you want to run your application.

## Step 3: Deploy Jenkins using Helm
Deploy Nginx on the Kubernetes cluster using Helm and you need to specify the release name in place of my-nginx and chart name
helm install <release-name> <chart-name>
e.g:
helm install my-nginx nginx-3replicas

## Access the Jenkins UI using loadbalancer svc:
- export SERVICE_IP=$(kubectl get svc --namespace default jenkins --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")
- echo http://$SERVICE_IP:8080/login

## Cleanup
To uninstall the Nginx chart:
helm uninstall <release-name>
- helm uninstall my-nginx

## Troubleshooting
If you encounter issues with the Nginx deployment, you can check the pod logs:
- kubectl logs <pod-name> -n namespace
