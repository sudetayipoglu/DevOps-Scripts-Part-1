📌 Introduction
<br><br>
This repository contains essential DevOps &amp; Cloud Engineering scripts for CI/CD and containerization. These scripts demonstrate best practices in DevOps and cloud automation, making this repository a valuable asset for any Cloud Engineer or DevOps professional.
# DevOps Scripts Part 1
🔹 CI/CD Pipeline Automation
GitLab CI/CD Pipeline - Node.js App Deployment
```yaml
stages:
  - test
  - build
  - deploy

test:
  stage: test
  script:
    - npm install   # Install dependencies
    - npm test      # Run tests

build:
  stage: build
  script:
    - npm run build  # Build the application

deploy:
  stage: deploy
  only:
    - main  # Deploy only when changes are pushed to the main branch
  script:
    - echo "Deploying to production..."
    - ssh user@server "cd /app && git pull && npm restart"  # Connect to server, pull latest code, restart app
```

✅ Usage: Commit changes to trigger the pipeline.

<br><br>
🔹 Containerization & Kubernetes
<br><br>
Dockerfile - Node.js Application
```yaml
# Use Node.js 18 as the base image
FROM node:18

# Set the working directory inside the container
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy application source code
COPY . .

# Define the command to start the app
CMD ["npm", "start"]

# Expose port 3000 for the application
EXPOSE 3000
```
✅ Usage:
```yaml
docker build -t myapp .   # Build the Docker image
docker run -p 3000:3000 myapp  # Run the container
```
<br><br>
Kubernetes Deployment
```yaml
# Define a Kubernetes Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 3  # Run 3 instances of the application
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:latest  # Use latest version of the image
        ports:
        - containerPort: 3000  # Expose port 3000
```
✅ Usage:
```yaml
kubectl apply -f deployment.yaml  # Deploy application to Kubernetes
kubectl get pods  # List running pods
```
🎯 **Conclusion**

This repository provides a comprehensive collection of scripts for DevOps, Cloud Engineering, and Automation. If you're preparing for a Cloud Engineer or DevOps role, these scripts will demonstrate your skills in Infrastructure as Code, CI/CD, Containerization, Security, and Monitoring.

✅ Star this repository ⭐ and start using these scripts in your DevOps projects! 🚀


