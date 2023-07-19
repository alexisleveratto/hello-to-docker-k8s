# Kubernetes 🚀

Kubernetes is a powerful container orchestration tool that simplifies the management of containerized applications in diverse environments. It offers key features for ensuring high availability, scalability, and disaster recovery.

## Architecture 🏢

Kubernetes follows a distributed architecture with multiple components working together:

                        ┌───────────┐
                        │   Master  │
                        │    Node   │
                        └───────────┘
                            |    |
                        ┌────┘─┌──┘───┐
                        │Worker│Worker│...
                        └──────┴──────┘


- The **Master Node** oversees the cluster and handles essential processes like the API server, controller manager, and scheduler.
- **Worker Nodes** host the applications, providing resources and executing the workload.

## Core Concepts 🧩

Kubernetes introduces several core concepts to manage containerized applications effectively:

+-------------+
|   Pod       |
+-------------+
|   Service   |
+-------------+
|   Ingress   |
+-------------+
|   ConfigMap |
+-------------+
|   Secrets   |
+-------------+
|   Volumes   |
+-------------+


- **Pod**: The smallest unit in Kubernetes that encapsulates one or more containers and shared resources. Pods offer an abstraction layer over containers, enabling flexible configurations and communication between containers within the same Pod.
- **Service**: Provides a stable network identity and a single access point for a set of Pods. Services enable communication between Pods, both internally and externally, and facilitate load balancing.
- **Ingress**: Manages external access to services within the cluster, serving as an entry point that routes incoming requests to the appropriate Services.
- **ConfigMap**: Stores configuration data separately from the application code, enabling easy modifications without rebuilding containers. ConfigMaps facilitate external configuration of applications.
- **Secrets**: Securely store sensitive information, such as API keys or passwords, required by applications. Secrets provide a safe mechanism for accessing and managing confidential data.
- **Volumes**: Enable data persistence and storage within Pods. Volumes can be used to store data on the local machine or remote storage, ensuring data survives container restarts or rescheduling.

## Deployment and StatefulSet 🚀

Kubernetes offers mechanisms to manage the lifecycle of applications efficiently:

- **Deployment**: Manages the creation, scaling, and updating of application replicas. Deployments ensure the desired number of replicas are running and handle rolling updates to minimize downtime during application changes.
- **StatefulSet**: Used for managing stateful applications that require stable network identities and persistent storage. StatefulSets ensure ordered and unique Pods, providing data persistence and consistency.

## Minikube 🖥️

Minikube is a local Kubernetes environment that simplifies testing and development on a single-node cluster. To start Minikube, use the following command: 

`minikube start --vm-driver=<VIRTUAL ENVIRONMENT TO USE>`

For example, to start Minikube with the Hyperkit driver, use `minikube start --vm-driver=hyperkit`.

## kubectl 💻

Kubectl is the command-line tool used to interact with Kubernetes clusters. Here are some useful commands:

- `kubectl get <K8s Component>`: Retrieve information about Kubernetes components.
- `kubectl create <K8s Component>`: Create Kubernetes components.
- `kubectl logs <POD_NAME>`: View logs of a Pod.
- `kubectl describe <K8s Component> <Component_NAME>`: Get detailed information about a Kubernetes component.
- `kubectl exec -it <POD_NAME> -- bin/bash`: Access a terminal inside a Pod.

## Config File and Deployment 📄

To apply a configuration file to a Kubernetes cluster, use the following command: `kubectl apply -f <FILE_PATH>`


This applies the configuration defined in the file to the cluster.

## Cleaning the Cluster 🧹

To clean up the cluster and remove resources, follow these steps:

1. `kubectl delete deployments,statefulsets,replicasets,pods --all`: Delete deployments, statefulsets, replicasets, and pods.
2. `kubectl delete services --all`: Delete services.

Remember to exercise caution when cleaning the cluster, as this action permanently removes resources.

## Complete Application Setup (e.g., MONGO) 🔄

To set up a complete application, such as MongoDB, in Kubernetes, follow these steps:

1. **Deployment | Pod**: Create the MongoDB deployment and pod. Example file: `mongodb-pod-deployment.yaml`.
2. **Secret**: Create a secret to store the admin user and password securely. Example file: `mongodb-secret.yaml`. Make sure to base64-encode the values.
3. **Service**: Create an internal service for MongoDB. Example file: `mongodb-internal-service-deployment.yaml`.
4. **Deployment | Pod** and **ConfigMap**: Create a ConfigMap for MongoDB configuration. Example file: `mongodb-configmap.yaml`. Then, create the Mongo Express pod and deployment. Example file: `mongo-express-pod-deployment.yaml`.
5. **Deployment | Service**: Create an external service for Mongo Express. Example file: `mongo-express-external-service.yaml`.

