# Deploying Tetris Game using ArgoCD on AWS EKS

## Introduction

In this guide, we will deploy a Tetris game using ArgoCD on an AWS EKS cluster. ArgoCD is a declarative, GitOps continuous delivery tool for Kubernetes.

## Pre-requisites

- AWS account with permissions to create EKS clusters and EC2 instances.
- Basic familiarity with AWS services, Kubernetes, and ArgoCD.
- Installed `kubectl` and `aws cli` on your local machine.

## Steps

1. **Create an EKS Cluster**: Set up an EKS cluster in your AWS account and add a node group where an EC2 instance will be created to run the cluster.

2. **Install kubectl and aws cli**: Install `kubectl` and `aws cli` on the EC2 instance where you will be managing the EKS cluster.

3. **Connect Instance with Cluster**: Configure the instance to connect with the EKS cluster using the command:
    ```bash
    aws eks update-kubeconfig --name "cluster_name" --region "region_name"
    ```

4. **Install ArgoCD**: Create a namespace for ArgoCD and install it using the provided YAML manifest:
    ```bash
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.4.7/manifests/install.yaml
    ```

5. **Expose ArgoCD Server**: Create a load balancer to expose the ArgoCD server and set its DNS in the ArgoCD server configuration.

6. **Login to ArgoCD**: Access the ArgoCD web page using the load balancer DNS, and log in with the default username `admin`. Retrieve the password as per the documentation.

7. **Connect Repository and Create Application**: Connect your Git repository to ArgoCD and create an application for deploying the Tetris game.

8. **Verify Deployment**: Check the status of the pods in the EKS instance using `kubectl get pods`. Ensure that the Tetris game pods are successfully created.

9. **Access the Tetris Game**: Obtain the host name from the ArgoCD service details and paste it into the browser to access the deployed Tetris game.

10. **Continuous Deployment**: Edit the deployment file to change the version of the game from v1 to v2. ArgoCD will automatically detect the change and trigger a deployment according to the updated deployment file.

## Conclusion

By following these steps, you have successfully deployed a Tetris game on an AWS EKS cluster using ArgoCD. The continuous deployment capabilities of ArgoCD ensure that any changes to the deployment files are automatically applied, providing a seamless deployment experience.

Feel free to contribute or report issues on GitHub.
