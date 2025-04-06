# Kubernetes-mini-project
this is a mini project on kubernetes .Understanding docker , kubernetes and microservices


Kubernetes Tutorial Projectflow
Prerequisites
Docker Desktop: Ensure Docker Desktop is installed and running.
Docker Hub: Sign in to Docker Hub.
Minikube: Install Minikube (instructions provided below).
Steps to Execute the Project
1. Build the Application
Create or use an existing application.
Test it locally to ensure it works as expected.
2. Prepare and Build the Docker Image
Create a Dockerfile in your project directory.
Build the Docker image:
docker build -t kubernetes-test-app:latest .
Verify the image:
docker images
Test the image locally:
docker run -p 5000:5000 kubernetes-test-app:latest
3. Create the Deployment YAML File
Define a Kubernetes deployment in a file named deployment.yaml.

4. Install Minikube
Visit the Minikube installation page: Minikube Installation Guide.
Download the .exe file and execute the installation via PowerShell as an administrator.
Restart your terminal after the installation (a system reboot may be required).
Start Minikube:

minikube start
# or
minikube start --embed-certs
5. Troubleshooting Minikube
Common Error
Failing to connect to https://registry.k8s.io/ from both inside the minikube container and host machine
To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
Solutions
If using a proxy, configure it for Minikube:

minikube start --docker-env HTTP_PROXY=http://your-proxy:port --docker-env HTTPS_PROXY=https://your-proxy:port
If no proxy is being used, unset these environment variables:

unset HTTP_PROXY
unset HTTPS_PROXY
unset NO_PROXY
Test connectivity to registry.k8s.io:

nslookup registry.k8s.io
Example output:

Server:  dlinkrouter.local
Address:  192.168.0.1

Non-authoritative answer:
Name:    registry.k8s.io
Addresses:  2600:1901:0:bbc4::
          34.96.108.209
Clean up and restart Minikube:

minikube stop
minikube delete --all
6. Verify Minikube Status
Check the status of the Minikube cluster:

minikube status
Verify Kubernetes resources:

kubectl get all -A
kubectl get pods -A
kubectl get nodes -A
7. Adding Nodes
To add a new node to the cluster:

minikube start --nodes=2
# or
minikube start --nodes=2 --embed-certs
8. Load Docker Image to Minikube
Verify the Docker images:
minikube image list
docker images
Load the Docker image into Minikube:
minikube image load kubernetes-test-app:latest
9. Apply Deployment
Deploy the application:

kubectl apply -f deployment.yaml
To delete the deployment (if needed):

kubectl delete deployment kubernetes-test-app
10. Test the Application
Check Pods and Nodes:

kubectl get pods -A
kubectl get nodes -A
Delete a specific Pod (optional):

kubectl delete pod <pod-name/id>
Access the application service:

minikube service kubernetes-test-app
Open the Minikube dashboard:

minikube dashboard
11. Debugging and Logs
View Pod logs:

kubectl logs -f <pod-id>
Check Endpoints and Services:

kubectl get endpoints
kubectl get service
12. Load Testing with Postman
Use Postman to run performance tests:
Go to Collection > Runs > Performance > Run Performance Test.
Example: Fixed configuration with 10 users for 1 minute.
13. Stop Minikube
Stop the Minikube cluster:

minikube stop
14. Handling ImagePullBackOff Issue
If you encounter the ImagePullBackOff error:

Tag the Docker image with your Docker Hub username:
docker tag kubernetes-test-app:latest <your-dockerhub-username>/kubernetes-test-app:latest
Push the image to Docker Hub:
docker push <your-dockerhub-username>/kubernetes-test-app:latest