# TikTok Backend Assignment

This project is a scalable backend application built with Golang and Kubernetes. It consists of two main components: `http-server` and `rpc-server`. The `http-server` handles incoming HTTP requests from clients, while the `rpc-server` provides RPC-based services to fulfill those requests. The application can be easily scaled using Kubernetes to handle increased workload and provide high availability.

## Usage

To use the application and scale it using Kubernetes, follow these steps:

1. Clone the project repository from GitHub: [repository URL]

2. Navigate to the project directory:
    Find the docker-compose.yml file, change the configuration to build always and then run it.

3. Use Postman:
    POST localhost:8080/api/send
    {
    "chat": "user1:user2",
    "text": "Pikachuuuu",
    "sender": "user1"
    }

    To send message 

    GET localhost:8080/api/pull
    {
    "chat": "user1:user2",
    "cursor": 0,
    "limit": 10,
    "reverse": true
    }

    To retrieve all the messages.

4. Installed JMeter:
   Tested my application with it:
        No issues for 20 QPS.
        No issues for 1000QPS. 
        Starts to get some IO timeout > 5000QPS.
        Some scaling can be done probably after 1000QPS.

5. Scaling Elastically - using minikube

   I started by building Docker images for both my HTTP server and RPC server applications using the docker build command. I tagged the images appropriately for each application.

   To ensure scalability, I pushed the Docker images to a local registry. I used the docker push command and made sure the registry was running and accessible.

   I created deployment YAML files (http-server-deployment.yaml and rpc-server-deployment.yaml) to define the deployments and autoscaling configurations for each application. In the YAML files, I specified the respective images for each application, such as localhost:5000/http-server-image and localhost:5000/rpc-server-image, reflecting the images in my local registry.

   I configured the resource limits and requests in the YAML files to define the CPU requirements for each application.

   To enable autoscaling for each application, I included an autoscaling section in each YAML file. I set the scaleTargetRef to point to the respective deployments and specified the minimum and maximum number of replicas using minReplicas and maxReplicas respectively.

   I defined the threshold for autoscaling based on CPU usage by setting the targetCPUUtilizationPercentage.

   Using the kubectl apply command, I applied the deployment YAML files to create the deployments and enable autoscaling for both the HTTP server and RPC server applications.

   To test the scalability and performance of both applications, I used JMeter, an open-source load testing tool. I configured JMeter to simulate multiple concurrent users and requests for each application to assess how they handled the load.

   I monitored the performance and scaling of both applications using the Minikube Dashboard. The dashboard provided real-time insights into the deployments, including the number of replicas, CPU usage, and other relevant metrics for both the HTTP server and RPC server applications.

By following the above steps, you can use and scale your backend application built with Golang and Kubernetes. Kubernetes simplifies the deployment and scaling process, allowing you to handle increased traffic, provide high availability, and easily adjust the number of replicas based on demand.

---
