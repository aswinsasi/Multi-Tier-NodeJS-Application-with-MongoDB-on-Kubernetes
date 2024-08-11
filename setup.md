Certainly! Here’s a document outlining the steps for creating the setup for deploying a multi-tier NodeJS application with MongoDB on a Kubernetes cluster:

---

# **Kubernetes Deployment Guide for NodeJS Application with MongoDB**

## **Objective**

Deploy a multi-tier NodeJS application with a MongoDB database on a Kubernetes cluster using the CLI. The NodeJS application is available as a Docker image on Docker Hub (`devopsedu/employee`), and MongoDB is available as a Docker image (`mongo:4.0`).

## **Prerequisites**

- Kubernetes cluster up and running.
- `kubectl` CLI tool installed and configured.
- Docker images available on Docker Hub.

## **Step 1: Create MongoDB Deployment and Service**

### **1.1 MongoDB Deployment**

Create a file named `mongo-deployment.yaml` with the following content:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      labels:
        app: mongo
    spec:
      containers:
      - name: mongo
        image: mongo:4.0
        ports:
        - containerPort: 27017
        volumeMounts:
        - name: mongo-storage
          mountPath: /data/db
      volumes:
      - name: mongo-storage
        emptyDir: {}
```

### **1.2 MongoDB Service**

Create a file named `mongo-service.yaml` with the following content:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongo
spec:
  selector:
    app: mongo
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
  type: ClusterIP
```

## **Step 2: Create NodeJS Deployment and Service**

### **2.1 NodeJS Deployment**

Create a file named `nodejs-deployment.yaml` with the following content:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: employee-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: employee-app
  template:
    metadata:
      labels:
        app: employee-app
    spec:
      containers:
      - name: nodejs
        image: devopsedu/employee
        ports:
        - containerPort: 8888
        env:
        - name: MONGO_URL
          value: "mongodb://mongo:27017"
```

### **2.2 NodeJS Service**

Create a file named `nodejs-service.yaml` with the following content:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: employee-app
spec:
  selector:
    app: employee-app
  ports:
    - protocol: TCP
      port: 8888
      targetPort: 8888
  type: LoadBalancer
```

## **Step 3: Apply Kubernetes Configurations**

### **3.1 Apply MongoDB Deployment and Service**

Run the following commands to deploy MongoDB:

```sh
kubectl apply -f mongo-deployment.yaml
kubectl apply -f mongo-service.yaml
```

### **3.2 Apply NodeJS Deployment and Service**

Run the following commands to deploy the NodeJS application:

```sh
kubectl apply -f nodejs-deployment.yaml
kubectl apply -f nodejs-service.yaml
```

## **Step 4: Verify Deployment**

### **4.1 Check Pods**

Verify that your pods are running:

```sh
kubectl get pods
```

### **4.2 Check Services**

Verify that your services are exposed:

```sh
kubectl get services
```

### **4.3 Access the NodeJS Application**

Obtain the external IP address of the NodeJS service:

```sh
kubectl get services employee-app
```

Use this IP address to access the NodeJS application.

## **Step 5: Test the Application**

### **5.1 Add an Employee**

Access the NodeJS application via the provided IP and port, and use the endpoint to add an employee.

### **5.2 Verify the Employee**

Go to the "Get Employee" page in the application and verify if the newly added employee appears.

---

By following these steps, you will deploy a NodeJS application and MongoDB on your Kubernetes cluster, ensuring they are properly configured to communicate and are accessible as required.