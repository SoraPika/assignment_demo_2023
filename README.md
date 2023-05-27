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
    "text": "chuuuu",
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

5. Create a Kubernetes deployment using the provided deployment configuration file:
   ```
   $ kubectl apply -f deployment.yaml
   ```

   This command will create the necessary Kubernetes resources, including deployments and services, based on the configuration specified in `deployment.yaml`.

6. Check the status of the deployments:
   ```
   $ kubectl get deployments
   ```

   Ensure that the desired number of replicas for both `http-server` and `rpc-server` are running.

## Scaling the Application

To scale the application, you can adjust the number of replicas in the `deployment.yaml` file or use the `kubectl scale` command. Here's an example of scaling both `http-server` and `rpc-server` to 5 replicas:

```
$ kubectl scale deployment http-server --replicas=5
$ kubectl scale deployment rpc-server --replicas=5
```

Kubernetes will handle the scaling process by creating or terminating the necessary pods to match the desired replica count.

## Conclusion

By following the above steps, you can use and scale your backend application built with Golang and Kubernetes. Kubernetes simplifies the deployment and scaling process, allowing you to handle increased traffic, provide high availability, and easily adjust the number of replicas based on demand.

---
