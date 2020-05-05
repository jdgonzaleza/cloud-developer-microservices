# Microservices Application: Udagram

Udagram is a images application used to understand microservices architecture and clud development.

1. [The Simple Frontend](/udacity-c3-frontend)
2. [The RestAPI Feed Backend](/udacity-c3-restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/udacity-c3-restapi-user), a Node-Express user microservice.
### Prerequisites
You will need to have an AWS account as we will use it to create our infraestructure.

1. To create the infraestructure, we are going to use Kubeone and Terraform. Please follow the following guide: https://github.com/kubermatic/kubeone/blob/master/docs/quickstart-aws.md .

### Running the application with Kubernetes
1.
1. Create the following environment variables as thery are going to be used thought the project. Also, your AWS credentials must already be set in the ```~.aws/credentials``` file.
   ```
    export POSTGRESS_USERNAME=yourusername;
    export POSTGRESS_PASSWORD=yourpassword;
    export POSTGRESS_DB=postgresdbname;
    export POSTGRESS_HOST=postgreshost;
    export AWS_REGION=awsregion;
    export AWS_PROFILE=default;
    export AWS_BUCKET=udagramdemo;
    export JWT_SECRET=helloworld;
   ```

1. Create a CREDENTIALS environment variable with the output of running the following command:
   ```
    cat ~/.aws/credentials | base64
   ```
   ```
   export CREDENTIALS=output from the previous command
   ```

2. cd into the ```udacity-cr-deployment/k8s```
2. Define the kubernetes services:
   ```
   kubectl apply -f backend-feed-service.yaml
   kubectl apply -f backend-user-service.yaml
   kubectl apply -f frontend-service.yaml
   kubectl apply -f reverseproxy-service.yaml
   ```
3. Carry out the deployments:
   ```
   kubectl apply -f backend-user-deployment.yaml
   kubectl apply -f backend-user-deployment.yaml
   kubectl apply -f frontend-deployment.yaml
   kubectl apply -f reverseproxy-deployment.yaml
   ```
4. Check that all the pods are running:
   ```
   kubectl get pod
   ```
5. To test locally run:
   ```
   kubectl port-forward service/frontend 8100:8100
   kubectl port-forward service/reverseproxy 8080:8080
   ```
6. Open  ```http://localhost:8100/``` to see the application running
