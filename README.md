Install Minikube on Ubuntu (Correct Way)

Step 1: Download Minikube
Run the following command to download the latest Minikube binary:
<curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 >

Step 2: Install Minikube
Move the downloaded file to /usr/local/bin and make it executable:
<sudo install minikube-linux-amd64 /usr/local/bin/minikube >

Verify the installation:
<minikube version >

Step 3: Start Minikube
Start Minikube with the default driver:
<minikube start --driver=docker
If you see an error about missing Docker, install it using:
sudo apt update && sudo apt install -y docker.io >

Step 4: Verify Minikube is Running
<minikube status >
If everything is working, you should see:

host: Running
kubelet: Running
apiserver: Running

Step 5: Test Kubernetes with Minikube
Try running a simple pod:

<kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
kubectl expose deployment hello-minikube --type=NodePort --port=8080
minikube service hello-minikube >


Test in a locaL monikube cluster using rolling update and rollback process

Step 1: Start Minikube
First, ensure that Minikube is installed. If not, install it from Minikube’s official page.

Start Minikube:
<minikube start >

Verify that Minikube is running:
<minikube status >

Step 2: Create a Deployment
Create a YAML file named deployment.yaml:

Apply the deployment:
<kubectl apply -f deployment.yaml >
Verify that the Pods are running:
<kubectl get pods >

Step 3: Expose the Deployment
Expose the Deployment to access it via a NodePort:
<kubectl expose deployment my-app --type=NodePort --port=80 >
Get the Minikube service URL:
<minikube service my-app --url >

Open the app in a browser:
<minikube service my-app >

Step 4: Perform a Rolling Update
Update the deployment to use nginx:1.20:
<kubectl set image deployment my-app my-container=nginx:1.20 >

Check the rollout status:
<kubectl rollout status deployment my-app >

Confirm that new Pods are running the updated version:
<kubectl get pods -o wide >

Step 5: Rollback if Needed
If the update fails or has issues, rollback to the previous version:
<kubectl rollout undo deployment my-app >

Check the rollback status:
<kubectl rollout status deployment my-app >

To see the revision history:
<kubectl rollout history deployment my-app >

Step 6: Clean Up
Once done, delete everything:
<kubectl delete deployment my-app
kubectl delete service my-app
minikube stop >


Install kubectl with --classic
Run the following command instead:
<sudo snap install kubectl --classic >

After installation, verify that kubectl is installed correctly:
<kubectl version --client >

Alternative: Install kubectl via APT (Recommended)
If you prefer not to use Snap, you can install kubectl from the official Kubernetes APT repository:

1️⃣ Add the Kubernetes repository
<sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl
curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo tee /usr/share/keyrings/kubernetes-archive-keyring.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list >

2️⃣ Install kubectl
<sudo apt update
sudo apt install -y kubectl >

3️⃣ Verify installation
<kubectl version --client >

🔥 Next Steps
✅ If you successfully install kubectl, try running:
<kubectl get nodes >
If Minikube is running, this command should show your local cluster.
# my_minikube
