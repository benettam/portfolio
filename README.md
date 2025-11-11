# Exp1a - Git Essentials Lab

## 🧩 **EXP 1 — Git Essentials**

### 📁 Step 1 — Create project folder

mkdir Exp1_Git
cd Exp1_Git


### 🧠 Step 2 — Initialize Git

git init


### 📝 Step 3 — Create a sample file

echo "Welcome to DevOps Lab - Exp 1" > README.md

### 🧾 Step 4 — Add file to staging area

git add .

### 💬 Step 5 — Commit changes

git commit -m "Initial commit - Added README file"

### 🌐 Step 6 — Connect local repo to GitHub

(Use your GitHub repository URL here 👇)

```bash
git remote add origin https://github.com/benettam/myrepo.git

### 🌳 Step 7 — Rename main branch (optional)

git branch -M main


### 🚀 Step 8 — Push to GitHub

```bash
git push -u origin main

### ✅ Step 9 — Check status

```bash
git status


### 💡 (Optional) Step 10 — View commit history




### **EXP NO: 2 — Docker Containers and Images**

### 🧱 **STEP 1 — Create project folder**

```bash
mkdir docker-demo
cd docker-demo
```

---

### 📝 **STEP 2 — Create a simple web page**

Create a file named `index.html`:

```bash
echo "<h1>Welcome to DevOps Lab Exam</h1>" > index.html
```

You can check the file content:

```bash
cat index.html
```

Expected output:

```
<h1>Welcome to DevOps Lab Exam</h1>
```

---

### 🐳 **STEP 3 — Create a Dockerfile**

Create the file named `Dockerfile` (no extension):

```bash
notepad Dockerfile
```

Paste the following inside 👇

```dockerfile
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
```

💾 Save and close the file.

---

### 🧠 **STEP 4 — Build the Docker image**

Now build your custom image:

```bash
docker build -t myweb:v1 .
```

✅ Output should end with:

```
Successfully built <image_id>
Successfully tagged myweb:v1
```

Check your image:

```bash
docker images
```

---

### 🚀 **STEP 5 — Run the Docker container**

```bash
docker run -d -p 8080:80 myweb:v1
```

✅ Output example:

```
Container ID: 8bfa4d3b9f2a...
```

Check running containers:

```bash
docker ps
```

Expected output:

```
CONTAINER ID   IMAGE      PORTS                 NAMES
8bfa4d3b9f2a   myweb:v1   0.0.0.0:8080->80/tcp  myweb-container
```

---

### 🌐 **STEP 6 — View in browser**

Open your browser and go to:

```
http://localhost:8080
```

✅ You should see the message:

```
Welcome to DevOps Lab Exam
```

---

### 🧹 **STEP 7 — Stop and remove container (optional cleanup)**

```bash
docker ps
docker stop <container_id>
docker rm <container_id>
```

To remove the image:

```bash
docker rmi myweb:v1
```

---

### ✅ 

## 🧩 **EXP NO: 3 — Flask App Containerization and Docker Hub Deployment**

## 🧱 **STEP 1 — Create your project folder**

mkdir flask-app
cd flask-app

## 🧾 **STEP 2 — Create Flask application file**

Create a file named `app.py`:

notepad app.py

from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return """
    <html>
    <head>
        <title>DevOps Lab Exam</title>
        <style>
            body { background-color: lightblue; text-align: center; font-family: Arial; padding-top: 100px; }
            h1 { color: navy; }
        </style>
    </head>
    <body>
        <h1>Welcome to DevOps Lab Exam</h1>
        <p>Containerized Flask Application</p>
    </body>
    </html>
    """
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)


## 🧩 **STEP 3 — Create requirements.txt**

echo Flask==2.2.5 > requirements.txt


## 🐳 **STEP 4 — Create Dockerfile**

notepad Dockerfile

FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]

## ⚙️ **STEP 5 — Build the Docker image**

docker build -t flask-app:v1 .


✅ Output:

```
Successfully built <image_id>
Successfully tagged flask-app:v1
```

Check your image:

```bash
docker images
```

---

## 🚀 **STEP 6 — Run the container**

If port 5000 is free:

docker run -p 5000:5000 flask-app:v1


If port 5000 is in use, try:

```bash
docker run -p 5050:5000 flask-app:v1
```

✅ Output:

```
 * Running on http://0.0.0.0:5000/
```

---

## 🌐 **STEP 7 — View in your browser**

Open your browser and visit:

```
http://localhost:5000
```

or (if used 5050)

```
http://localhost:5050
```

✅ You should see a simple blue page:

```
Welcome to DevOps Lab Exam
Containerized Flask Application
```

---

## 🐋 **STEP 8 — (Optional) Push to Docker Hub**

1. **Login to Docker Hub**

```bash
docker login
```

2. **Tag your image** (replace `<your-username>` with your Docker Hub username)

```bash
docker tag flask-app:v1 benettam471/flask-app:latest
```

3. **Push it to Docker Hub**

```bash
docker push benettam471/flask-app:latest
```

✅ Check it on:
👉 [https://hub.docker.com/repositories](https://hub.docker.com/repositories)

---

## 🧹 **STEP 9 — Cleanup (optional)**

To stop container:

```bash
docker ps
docker stop <container_id>
docker rm <container_id>
```

To delete image:

```bash
docker rmi flask-app:v1
```



# 🧩 **EXP NO: 4 — Jenkins Deployment Using Docker**
## 🧱 **STEP 1 — Create project folder**

mkdir jenkins-app
cd jenkins-app
```

---

## 🧾 **STEP 2 — Create Docker Compose file**

Create file `docker-compose.yml`:

```bash
notepad docker-compose.yml
```

Paste this code 👇

```yaml
version: '3.8'
services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins
    restart: unless-stopped
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock

volumes:
  jenkins_home:
```

💾 Save and close.

---

## 🚀 **STEP 3 — Start Jenkins Container**

Run:

```bash
docker compose up -d
```

✅ Output:

```
✔ Container jenkins  Started
```

Check running container:

```bash
docker ps
```

You’ll see:

```
CONTAINER ID   IMAGE                PORTS
xxxxxx         jenkins/jenkins:lts  0.0.0.0:8080->8080/tcp
```

---

## 🔑 **STEP 4 — Get Jenkins Admin Password**

Run:

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Copy the displayed password.

---

## 🌐 **STEP 5 — Access Jenkins**

1. Open your browser → Go to
   👉 [http://localhost:8080](http://localhost:8080)
2. Paste the admin password.
3. Choose **Install Suggested Plugins**.
4. Create an admin username and password.

---

## 🧩 **STEP 6 — Install Plugin**

Inside Jenkins:

* Go to **Manage Jenkins → Plugins → Available Plugins**
* Search and install **HTML Publisher Plugin**
* Restart Jenkins if prompted.

---

## 🧠 **STEP 7 — Create a New Pipeline**

1. Click **New Item → Pipeline → OK**
2. Scroll to **Pipeline Script** section
3. Paste the below simple Jenkinsfile 👇

---

### 📝 **Pipeline Script**

```groovy
pipeline {
  agent any
  stages {
    stage('Generate Page') {
      steps {
        script {
          sh 'mkdir -p site'
          writeFile file: 'site/index.html', text: """
          <html>
          <head><title>DevOps Lab Exam</title></head>
          <body style='text-align:center;font-family:Arial;background:lightblue;padding-top:100px;'>
            <h1>Welcome to DevOps Lab Exam</h1>
            <p>Generated by Jenkins Pipeline</p>
          </body>
          </html>
          """
        }
      }
    }
    stage('Publish Page') {
      steps {
        publishHTML([reportDir: 'site', reportFiles: 'index.html', reportName: 'DevOps Lab Site'])
      }
    }
  }
}
```

💾 Click **Save**.

---

## ▶️ **STEP 8 — Run Pipeline**

Click **Build Now**

✅ Green Tick ✔️ → means build successful.

---

## 🌍 **STEP 9 — View Output**

1. Click the latest **Build Number (#1)**
2. On the left panel → Click **DevOps Lab Site**

✅ Output webpage appears:

```
Welcome to DevOps Lab Exam
Generated by Jenkins Pipeline
```

---

## 🧹 **STEP 10 — Stop Jenkins (optional)**

```bash
docker stop jenkins
docker rm jenkins
docker volume rm jenkins-app_jenkins_home
```


# 🧩 **EXP NO: 5 — CI Pipeline using GitHub Actions and Docker Hub**


## 🧱 **STEP 1 — Create a Project Folder**

```bash
mkdir python-ci-lab
cd python-ci-lab
```

---

## 🧾 **STEP 2 — Create Required Files**

### 1️⃣ `app.py`

```python
def add(a, b):
    return a + b

if __name__ == "__main__":
    print("Welcome to DevOps Lab Exam!")
    print("2 + 3 =", add(2, 3))
```

---

### 2️⃣ `test_app.py`

```python
from app import add

def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0
```

---

### 3️⃣ `requirements.txt`

```
pytest
```

---

### 4️⃣ `Dockerfile`

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

---

## 🧠 **STEP 3 — Test Locally (Optional)**

```bash
python app.py
pytest -q
docker build -t python-ci-lab:v1 .
docker run python-ci-lab:v1
```

✅ Output:

```
Welcome to DevOps Lab Exam!
2 + 3 = 5
```

---

## 🌐 **STEP 4 — Create a GitHub Repository**

1. Go to **[https://github.com/](https://github.com/)**
2. Click **New Repository**
3. Name it → `python-ci-lab`
4. Keep it **Public**
5. Click **Create Repository**

---

## 🔁 **STEP 5 — Push Your Project to GitHub**

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/benettam/python-ci-lab.git
git push -u origin main
```

---

## ⚙️ **STEP 6 — Add GitHub Actions Workflow**

Create folders:

```bash
mkdir -p .github/workflows
```

Then create workflow file:

```bash
notepad .github/workflows/ci.yml
```

Paste this 👇

```yaml
name: CI Pipeline

on:
  push:
    branches: [ "main" ]

jobs:
  build-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - run: pip install -r requirements.txt
      - run: pytest -q
```

💾 Save and close the file.

---

## 🧭 **STEP 7 — Commit and Push Workflow**

```bash
git add .github/workflows/ci.yml
git commit -m "Add CI workflow"
git push
```

---

## 🚀 **STEP 8 — View CI Pipeline on GitHub**

1. Go to your **GitHub repo**
2. Click the **Actions** tab
3. A workflow called **CI Pipeline** will start automatically
4. Wait for the **Green Tick (✔️)**

✅ Output:

```
All tests passed successfully!
```

---

## 🐳 **STEP 9 — (Optional) Push Docker Image to Docker Hub**

### 1️⃣ Login to Docker Hub

```bash
docker login
```

### 2️⃣ Tag your image

```bash
docker tag python-ci-lab:v1 benettam/python-ci-lab:latest
```

### 3️⃣ Push it to Docker Hub

```bash
docker push benettam/python-ci-lab:latest
```

✅ Now your image is live on Docker Hub
Check:
👉 [https://hub.docker.com/repositories](https://hub.docker.com/repositories)

---

## 🔑 **STEP 10 — Add GitHub Secrets (if automating Docker push)**

Go to:
**Repo → Settings → Secrets and variables → Actions → New repository secret**

Add:

* `DOCKERHUB_USERNAME` → your Docker username
* `DOCKERHUB_TOKEN` → Docker Hub Access Token

You can generate the token from:
👉 [https://hub.docker.com/settings/security](https://hub.docker.com/settings/security)

---

 🧾 RESULT**

✅ Successfully created and executed a **CI Pipeline** using **GitHub Actions** that:



# 🧩 **EXP NO: 6 — Manage Kubernetes Resources using CLI**

**STEP 1 — Verify Setup**

Start Minikube:

```bash
minikube start --driver=docker
```

Check node status:

```bash
kubectl get nodes
```

✅ Output:

```
NAME           STATUS   ROLES           AGE   VERSION
minikube       Ready    control-plane   2m    v1.34.0
```

---

## 🧩 **STEP 2 — Create a Simple Pod**

Create file `nginx-pod.yaml`:

```bash
notepad nginx-pod.yaml
```

Paste this 👇

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```

Apply it:

```bash
kubectl apply -f nginx-pod.yaml
```

Check pod:

```bash
kubectl get pods
```

✅ Output:

```
NAME         READY   STATUS    RESTARTS   AGE
nginx-pod    1/1     Running   0          20s
```

To see details:

```bash
kubectl describe pod nginx-pod
```

Access app locally:

```bash
kubectl port-forward pod/nginx-pod 8080:80
```

Then open in browser:
👉 [http://localhost:8080](http://localhost:8080)

✅ You’ll see the **“Welcome to Nginx”** page.

Delete the pod:

```bash
kubectl delete pod nginx-pod
```

---

## 🧩 **STEP 3 — Create a Deployment**

```bash
kubectl create deployment my-nginx --image=nginx
```

Check deployment:

```bash
kubectl get deployments
kubectl get pods
```

Scale the deployment:

```bash
kubectl scale deployment my-nginx --replicas=3
kubectl get pods
```

✅ Output:

```
NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/my-nginx    3/3     3            3           1m
```

---

## 🧩 **STEP 4 — Expose Deployment as a Service**

Expose service:

```bash
kubectl expose deployment my-nginx --type=NodePort --port=80
```

Check services:

```bash
kubectl get svc
```

✅ Output:

```
NAME            TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
my-nginx        NodePort   10.102.55.10   <none>        80:30080/TCP   10s
```

Get service URL:

```bash
minikube service my-nginx --url
```

Open that URL in your browser —
✅ It shows the **Nginx Welcome Page.**

---

## 🧩 **STEP 5 — Update the Deployment (Rolling Update)**

```bash
kubectl set image deployment/my-nginx nginx=nginx:1.25
kubectl rollout status deployment/my-nginx
```

If something goes wrong:

```bash
kubectl rollout undo deployment/my-nginx
```

---

## 🧩 **STEP 6 — Cleanup**

```bash
kubectl delete deployment my-nginx
kubectl delete svc my-nginx
minikube stop
minikube delete
```

---


Perfect 👍 Benetta — here’s your **Experiment No: 7 — Kubernetes Deployment and Service for a Python App (from Docker Hub)**
I’ve written it in a **clean, exam-ready format** (AIM → Tools → Procedure → Commands → Output → Result).
This experiment extends Exp 6 — deploying your **Python/Flask app image** from Docker Hub onto Kubernetes using **Minikube**.

---

# 🧩 **EXP NO: 7 — Kubernetes Deployment and Service for Python App from Docker Hub**


## 🧱 **STEP 1 — Verify Cluster Setup**

Start Minikube:

```bash
minikube start --driver=docker
```

Check if the node is ready:

```bash
kubectl get nodes
```

✅ Output:

```
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   2m    v1.34.0
```

---

## 🧩 **STEP 2 — Pull a Python App Image from Docker Hub**

You can use any public image.
Here we’ll use a Flask app sample:

```bash
docker pull dockersamples/flaskapp
```

✅ Output:

```
Status: Downloaded newer image for dockersamples/flaskapp:latest
```

---

## 🧾 **STEP 3 — Create Deployment YAML File**

Create file:

```bash
notepad python-deployment.yaml
```

Paste this 👇

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: python-web-deployment
  labels:
    app: python-web
spec:
  replicas: 2
  selector:
    matchLabels:
      app: python-web
  template:
    metadata:
      labels:
        app: python-web
    spec:
      containers:
      - name: python-web
        image: dockersamples/flaskapp:latest
        ports:
        - containerPort: 5000
```

Apply the deployment:

```bash
kubectl apply -f python-deployment.yaml
```

Check status:

```bash
kubectl get deployments
kubectl get pods
```

✅ Output:

```
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
python-web-deployment   2/2     2            2           30s
```

---

## 🌐 **STEP 4 — Expose the Deployment as a Service**

Create file:

```bash
notepad python-service.yaml
```

Paste this 👇

```yaml
apiVersion: v1
kind: Service
metadata:
  name: python-web-service
spec:
  type: NodePort
  selector:
    app: python-web
  ports:
  - protocol: TCP
    port: 5000
    targetPort: 5000
```

Apply it:

```bash
kubectl apply -f python-service.yaml
```

Check services:

```bash
kubectl get svc
```

✅ Output:

```
NAME                 TYPE       CLUSTER-IP      PORT(S)          AGE
python-web-service   NodePort   10.109.140.21   5000:32214/TCP   10s
```

---

## 🌍 **STEP 5 — Access the Application**

Get the service URL:

```bash
minikube service python-web-service --url
```

✅ Example Output:

```
http://192.168.49.2:32214
```

Now open that URL in your browser.
You’ll see your **Python Flask Web App** running from **Kubernetes Cluster**. 🎉

---

## 🧹 **STEP 6 — Clean Up Resources**

To delete all created resources:

```bash
kubectl delete -f python-deployment.yaml
kubectl delete -f python-service.yaml
```

Or to stop the cluster completely:

```bash
minikube stop
minikube delete
```

---

## 🧾 **RESULT**

Successfully deployed a **Python web application** from **Docker Hub** to a **Kubernetes cluster**,
exposed it as a **Service**, and accessed it via **Minikube** URL.

---

## ✅ **OUTPUT SCREEN (Expected)**

**Browser Output:**

```
Welcome to Flask Sample Application
```

**Terminal Output:**

```
NAME                    READY   STATUS    RESTARTS   AGE
python-web-deployment   2/2     Running   0          1m
python-web-service      NodePort   10.109.140.21   5000:32214/TCP   30s
```

---
