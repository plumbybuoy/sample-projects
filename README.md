This setup should get Jenkins running on a Kubernetes cluster with external access through a Load Balancer. 

### Step 1: Create a Namespace for Jenkins
Create a separate namespace for Jenkins to isolate its resources:
```sh
kubectl create namespace jenkins
```

### Step 2: Add Helm Repository for Jenkins
Add the official Jenkins Helm chart repository and update it:
```sh
helm repo add jenkinsci https://charts.jenkins.io
helm repo update
```

### Step 3: Install Jenkins with Helm
Use Helm to deploy Jenkins into your cluster with a LoadBalancer service. Here’s an example of the installation command with default configurations:
```sh
helm install jenkins jenkinsci/jenkins \
  --namespace jenkins \
  --set controller.serviceType=LoadBalancer \
  --set controller.servicePort=8080
```

### Step 4: Wait for the Load Balancer IP
It may take a few minutes for the LoadBalancer to get an external IP. Check the IP with:
```sh
kubectl get svc -n jenkins
```
Once you see an external IP under `EXTERNAL-IP`, you can access Jenkins at `http://<external-ip>:8080`.
