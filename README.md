# Kubernetes Mini Project 🚀

This is a mini project designed to help you understand **Docker**, **Kubernetes**, and **Microservices**. It walks you through building, containerizing, deploying, and testing a simple application using Kubernetes with Minikube.

---

## 📚 Prerequisites

Make sure the following tools are installed and configured on your system:

1. **Docker Desktop** – Ensure it's installed and running.  
2. **Docker Hub** – Sign in to your Docker Hub account.  
3. **Minikube** – Install Minikube (instructions provided below).

---

## 🛠️ Project Workflow

### 1. Build the Application

- Create or use an existing application (e.g., a simple Flask or Node.js app).
- Test it locally to ensure it works as expected.

---

### 2. Prepare and Build the Docker Image

- Create a `Dockerfile` in your project directory.
- Build the Docker image:

  ```bash
  docker build -t kubernetes-test-app:latest .
  ```

- Verify the image:

  ```bash
  docker images
  ```

- Run and test the image locally:

  ```bash
  docker run -p 5000:5000 kubernetes-test-app:latest
  ```

---

### 3. Create Kubernetes Deployment YAML

- Define your deployment configuration in a file named `deployment.yaml`.

---

### 4. Install Minikube

- Visit the [Minikube Installation Guide](https://minikube.sigs.k8s.io/docs/start/).
- Download the executable and install it via PowerShell (Run as Administrator).
- Restart your terminal or system if needed.

Start Minikube:

```bash
minikube start
# or
minikube start --embed-certs
```

---

### 5. Troubleshooting Minikube

#### ❌ Common Error

Failing to connect to `https://registry.k8s.io/`.

#### ✅ Solutions

If using a proxy:

```bash
minikube start --docker-env HTTP_PROXY=http://your-proxy:port --docker-env HTTPS_PROXY=https://your-proxy:port
```

If **not** using a proxy:

```bash
unset HTTP_PROXY
unset HTTPS_PROXY
unset NO_PROXY
```

Test connectivity:

```bash
nslookup registry.k8s.io
```

#### Clean Up and Restart Minikube

```bash
minikube stop
minikube delete --all
```

---

### 6. Verify Minikube Status

- Check cluster status:

  ```bash
  minikube status
  ```

- Verify Kubernetes resources:

  ```bash
  kubectl get all -A
  kubectl get pods -A
  kubectl get nodes -A
  ```

---

### 7. Add More Nodes (Optional)

To create a multi-node cluster:

```bash
minikube start --nodes=2
# or
minikube start --nodes=2 --embed-certs
```

---

### 8. Load Docker Image into Minikube

- Check available Docker images:

  ```bash
  docker images
  ```

- Load your Docker image into Minikube:

  ```bash
  minikube image load kubernetes-test-app:latest
  ```

---

### 9. Apply Deployment

- Deploy your application:

  ```bash
  kubectl apply -f deployment.yaml
  ```

- To delete the deployment:

  ```bash
  kubectl delete deployment kubernetes-test-app
  ```

---

### 10. Test the Application

- View pods and nodes:

  ```bash
  kubectl get pods -A
  kubectl get nodes -A
  ```

- Delete a specific pod (optional):

  ```bash
  kubectl delete pod <pod-name>
  ```

- Access the application:

  ```bash
  minikube service kubernetes-test-app
  ```

- Launch the Minikube dashboard:

  ```bash
  minikube dashboard
  ```

---

### 11. Debugging and Logs

- View pod logs:

  ```bash
  kubectl logs -f <pod-name>
  ```

- Inspect endpoints and services:

  ```bash
  kubectl get endpoints
  kubectl get service
  ```

---

### 12. Load Testing with Postman

- Use **Postman** for performance testing:
  - Go to: `Collections > Runs > Performance > Run Performance Test`
  - Example: Run with 10 users for 1 minute.

---

### 13. Stop Minikube

To shut down the Minikube cluster:

```bash
minikube stop
```

---

### 14. Fixing ImagePullBackOff Errors

If you get an `ImagePullBackOff` error:

1. Tag the image with your Docker Hub username:

   ```bash
   docker tag kubernetes-test-app:latest <your-dockerhub-username>/kubernetes-test-app:latest
   ```

2. Push the image to Docker Hub:

   ```bash
   docker push <your-dockerhub-username>/kubernetes-test-app:latest
   ```

---

## 📦 Sample Folder Structure

```
kubernetes-mini-project/
│
├── app/
│   └── app.py
├── Dockerfile
├── deployment.yaml
├── README.md
```

---

