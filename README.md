# Application deployment on EKS through Github actions

<img width="747" height="599" alt="image" src="https://github.com/user-attachments/assets/55c040ad-d437-4656-b834-cead3abf7008" />

1.The developer commits the application’s code to the Source Code Repository. In this post we will leverage a repository created in AWS CodeCommit.

2.The commit to the Source Control Management (SCM) system triggers the AWS CodePipeline, which is the orchestration service that manages the CI/CD pipeline.

3.AWS CodePipeline proceeds to the Build stage, where AWS CodeBuild, integrated with GitHub Actions, builds the container image from the committed code.

4.Once the container image is successfully built, AWS CodeBuild, with GitHub Actions, pushes the image to Amazon Elastic Container Registry (ECR) for storage and versioning.

5.An Approval Stage is included in the pipeline, which allows the developer to manually review and approve the build artifacts before they are deployed.

6.After receiving approval, AWS CodePipeline advances to the Deploy Stage, where GitHub Actions are used to run helm deployment commands.

7.Within this Deploy Stage, AWS CodeBuild uses GitHub Actions to install the Helm application on Amazon Elastic Kubernetes Service (EKS), leveraging Helm charts for deployment.

8.The deployed application is now running on Amazon EKS and is accessible via the automatically provisioned Application Load Balancer.


# K8s manifest files

mongo-config.yaml

mongo-secret.yaml

mongo.yaml

webapp.yaml

# K8s commands

start Minikube and check status

minikube start --vm-driver=hyperkit 

minikube status



# get minikube node's ip address

minikube ip



# get basic info about k8s components

kubectl get node

kubectl get pod

kubectl get svc

kubectl get all



# get extended info about components

kubectl get pod -o wide

kubectl get node -o wide



# get detailed info about a specific component

kubectl describe svc {svc-name}

kubectl describe pod {pod-name}



#get application logs

kubectl logs {pod-name}



stop your Minikube cluster

minikube stop




⚠️ Known issue - Minikube IP not accessible

If you can't access the NodePort service webapp with MinikubeIP:NodePort, execute the following command:

minikube service webapp-service




# Links

mongodb image on Docker Hub: https://hub.docker.com/_/mongo

webapp image on Docker Hub: https://hub.docker.com/repository/docker/nanajanashia/k8s-demo-app

k8s official documentation: https://kubernetes.io/docs/home/

webapp code repo: https://gitlab.com/nanuchi/developing-with-docker/-/tree/feature/k8s-in-hour
