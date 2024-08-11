Certainly! Here's a GitHub repository description you can use for the project:

---

# **Multi-Tier NodeJS Application with MongoDB on Kubernetes**

## **Overview**

This repository contains configurations for deploying a multi-tier NodeJS application with MongoDB on a Kubernetes cluster. The setup includes a NodeJS application that connects to a MongoDB database, both deployed and managed within Kubernetes. The NodeJS application is available as a Docker image (`devopsedu/employee`), and MongoDB is available as a Docker image (`mongo:4.0`).

## **Features**

- **NodeJS Application**: Deployed on Kubernetes with an external IP for access.
- **MongoDB**: Deployed as a service in Kubernetes, providing internal access for the NodeJS application.
- **Deployment Configurations**: Includes YAML files for deploying MongoDB and NodeJS application, as well as their respective services.
- **External Access**: The NodeJS application is exposed via a LoadBalancer service, providing external access for testing and interaction.

## **Setup**

### **Prerequisites**

- Kubernetes cluster up and running.
- `kubectl` CLI tool installed and configured.
- Access to Docker Hub to pull required images.

### **Deployment Steps**

1. **Create MongoDB Deployment and Service**
   - **mongo-deployment.yaml**: Defines the MongoDB deployment with a persistent volume.
   - **mongo-service.yaml**: Defines the MongoDB service for internal access.

2. **Create NodeJS Deployment and Service**
   - **nodejs-deployment.yaml**: Defines the NodeJS application deployment with environment variables.
   - **nodejs-service.yaml**: Defines the NodeJS service with external LoadBalancer for access.

3. **Apply Kubernetes Configurations**
   - Use `kubectl apply -f <filename>` to create deployments and services.

4. **Verify Deployment**
   - Check pod and service statuses using `kubectl get pods` and `kubectl get services`.
   - Access the NodeJS application using the external IP provided by the LoadBalancer service.

5. **Test the Application**
   - Add an employee through the NodeJS application.
   - Verify employee data by accessing the "Get Employee" page.

## **Files**

- **mongo-deployment.yaml**: Kubernetes deployment configuration for MongoDB.
- **mongo-service.yaml**: Kubernetes service configuration for MongoDB.
- **nodejs-deployment.yaml**: Kubernetes deployment configuration for the NodeJS application.
- **nodejs-service.yaml**: Kubernetes service configuration for the NodeJS application.

## **License**

This project is licensed under the [MIT License](LICENSE).

## **Contributing**

Feel free to open issues or submit pull requests if you have suggestions or improvements.

## **Contact**

For any questions or support, please contact [aswinsasi](mailto:aswinfear01@gmail.com).

---

Feel free to adjust any sections to better match your specific project details or preferences!
