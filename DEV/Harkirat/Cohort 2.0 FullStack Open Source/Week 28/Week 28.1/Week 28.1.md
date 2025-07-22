In this lecture, Harkirat explores the practical aspects of deploying Kubernetes in different environments. He demonstrates how to run Kubernetes clusters locally and on cloud providers, highlighting the key differences and considerations for each approach. The lecture then addresses the limitations of Kubernetes Services, introducing Ingress as a solution for more advanced traffic routing. Harkirat delves into the concept of Ingress controllers, with a focus on installing and configuring the NGINX Ingress controller.

  

Kubernetes 2

What We've Covered Already

Today's Topics

Tomorrow's Topics

Future Topics (Offline Video)

Recapping Already Covered

Recapping How to Run Kubernetes Locally

1] Creating a Cluster

2] Creating a Pod

3] Creating a ReplicaSet

4] Creating a Deployment

Key Takeaways

How to Run Kubernetes on a Cloud Provider

Step 1: Create a Kubernetes Cluster

Step 2: Configure kubectl

Step 3: Create a Deployment

Key Points

Services in Kubernetes

NodePort Service

LoadBalancer Service

Key Points

Downsides of Services

Practical Demonstration

Key Observations

Potential Solutions

Ingress and Ingress Controller

Ingress

Important Note:

Ingress Controller

Key Benefits of Using Ingress

Considerations

Ingress Controllers

Kubernetes Namespaces

Understanding Namespaces

Working with Namespaces

Creating Resources in a Namespace

Changing Default Namespace

Key Points

Installing the NGINX Ingress Controller

1. Install Helm

2. Add and Update the ingress-nginx Repository

3. Install NGINX Ingress Controller

4. Verify the Installation

5. Check the Created LoadBalancer Service

Key Points

Setting Up Ingress Routing

1. Clean Up Existing Resources

2. Create Combined Manifest

3. Apply the Manifest

4. Update Local Hosts File

5. Test the Setup

Key Components

Important Notes

Conclusion

Trying Traefik's Ingress Controller

1. Install Traefik Ingress Controller

2. Verify Installation

3. Create Traefik Ingress Resource

4. Update Local Hosts File

5. Test the Setup

Issue Identification

Assignment: Path Rewriting with Traefik

Key Points

Secrets and ConfigMaps

Kubernetes Configuration Best Practices

ConfigMaps and Secrets

Key Rule: Externalize Secrets

Using ConfigMaps and Secrets

Example: Creating and Using a ConfigMap

Example: Creating and Using a Secret

Benefits of Using ConfigMaps and Secrets

ConfigMaps

What is a ConfigMap?

Creating a ConfigMap

Creating an Express App with Environment Variables

Deploying the Express App in Kubernetes

Creating a Service for the Express App

Accessing the Application

Key Points

  

  

  

  

# Kubernetes 2

In this lecture, we'll build upon the foundational concepts of Kubernetes and explore more advanced topics. Let's review what we've covered so far and what we'll be learning today and in the upcoming sessions.

![Untitled 54.png](../../../../Images/Untitled%2054.png)

### What We've Covered Already

1. **Clusters**: The foundation of Kubernetes, comprising a set of nodes that run containerized applications.
2. **Nodes**: The individual machines (physical or virtual) that make up a Kubernetes cluster.
3. **Pods**: The smallest deployable units in Kubernetes, typically containing one or more containers.
4. **Deployments**: Higher-level abstractions that manage ReplicaSets and provide declarative updates for Pods.
5. **ReplicaSets**: Ensure a specified number of pod replicas are running at any given time.

### Today's Topics

1. **Namespaces**:
    - Virtual clusters within a physical cluster
    - Used for organizing and isolating resources
2. **Ingress**:
    - An API object that manages external access to services in a cluster
    - Typically HTTP
3. **Ingress Controllers**:
    - Implementation of Ingress
    - We'll cover two popular options:  
        a. NGINX Ingress Controller  
        b. Traefik  
        
4. **ConfigMaps**:
    - API objects used to store non-confidential data in key-value pairs
    - Can be consumed as environment variables, command-line arguments, or configuration files in a volume
5. **Secrets**:
    - Similar to ConfigMaps, but for storing sensitive information
    - Encoded in base64 by default

### Tomorrow's Topics

1. **Cert Management**:
    - Automating the management and issuance of TLS certificates in Kubernetes
2. **Volumes and Persistent Volumes**:
    - Storage abstraction in Kubernetes
    - Persistent Volumes provide a way to store data that outlives the lifetime of a pod
3. **Resource Management**:
    - Controlling and optimizing resource allocation for containers in a cluster

### Future Topics (Offline Video)

1. **Horizontal Pod Autoscaling (HPA)**:
    - Automatically adjusting the number of pods in a deployment or replicaset based on observed metrics
2. **Node Autoscaling**:
    - Automatically adjusting the number of nodes in a cluster based on resource demands
3. **Practical Labs**:
    - Applying Kubernetes concepts to a real codebase

  

As we progress, you'll see how these components work together to create robust, scalable, and manageable containerized applications. Each of these topics builds on the foundational concepts we've already covered, providing you with a comprehensive understanding of Kubernetes and its ecosystem.

> Remember, Kubernetes is a complex system with many interrelated parts. Don't worry if you don't grasp everything immediately – practice and hands-on experience are key to mastering these concepts.

  

  

  

# Recapping Already Covered

Let's review the key concepts we've covered in Kubernetes so far:

1. Cluster:
    - A Kubernetes cluster is a set of machines working together to deploy applications.
    - It consists of multiple nodes that collectively manage containerized workloads.
2. Nodes:  
    There are two types of nodes in a Kubernetes cluster:  
    a. Master Node (Control Plane):  
    - Exposes an API that developers use to deploy pods.
    - Manages the overall state of the cluster.  
        b. Worker Node:  
        
    - Actually runs the pods containing application containers.
3. Pods:
    - The smallest executable unit in a Kubernetes cluster.
    - Can run one or more containers.
    - Represents a single instance of an application.
4. ReplicaSets:
    - Allow creation of multiple pod replicas.
    - Ensure a specified number of pod replicas are running.
    - Handle pod failures by automatically replacing or restarting pods.
5. Deployments:
    - A higher-level abstraction that manages ReplicaSets.
    - Provides declarative updates for Pods and ReplicaSets.
    - Enables easy rolling updates and rollbacks of applications.
6. Services:  
    Services expose pods to other pods or to the internet. There are three types:  
    a. ClusterIP:  
    
    - Exposes the service on an internal IP within the cluster.
    
    b. NodePort:
    
    - Exposes the service on each Node's IP at a static port.
    
    c. LoadBalancer:
    
    - Creates an external load balancer in cloud providers that support it.
    - Automatically creates a NodePort and ClusterIP services to which the external load balancer routes.

  

  

  

  

# Recapping How to Run Kubernetes Locally

This section provides a step-by-step guide on setting up and running Kubernetes components locally using Kind (Kubernetes in Docker).

### 1] Creating a Cluster

1. Create a `kind.yml` file:

```YAML
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  extraPortMappings:
  - containerPort: 30007
    hostPort: 30007
- role: worker
  extraPortMappings:
  - containerPort: 30007
    hostPort: 30008
- role: worker
```

1. Create the cluster:

```Shell
kind create cluster --config kind.yml --name local2
```

1. Verify cluster creation:

```Shell
docker ps
```

### 2] Creating a Pod

1. Create `pod.yml`:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

1. Apply the pod manifest:

```Shell
kubectl apply -f pod.yml
```

1. Verify pod creation:

```Shell
kubectl get pods
```

1. Check pod logs:

```Shell
kubectl logs -f nginx
```

1. Delete the pod:

```Shell
kubectl delete pod nginx
```

### 3] Creating a ReplicaSet

1. Create `rs.yml`:

```YAML
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

1. Apply the ReplicaSet:

```Shell
kubectl apply -f rs.yml
```

1. Verify pod creation:

```Shell
kubectl get pods
```

1. Test self-healing by deleting a pod
2. Delete the ReplicaSet:

```Shell
kubectl delete rs nginx-replicaset
```

### 4] Creating a Deployment

1. Create `deployment.yml`:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

1. Apply the Deployment:

```Shell
kubectl apply -f deployment.yml
```

1. Check ReplicaSets:

```Shell
kubectl get rs
```

1. Check Pods:

```Shell
kubectl get pods
```

1. Test with incorrect image:
    - Update `deployment.yml` with `image: nginx2:latest`
    - Apply the updated deployment
    - Verify that old pods are still running:
        
        ```Shell
        kubectl get pods
        ```
        

### Key Takeaways

1. Kind allows easy local Kubernetes cluster setup.
2. Pods are the smallest deployable units.
3. ReplicaSets ensure a specified number of pod replicas are running.
4. Deployments manage ReplicaSets and provide declarative updates.
5. Deployments maintain application availability during updates.

Remember to keep the deployment running for future exercises.

  

  

# How to Run Kubernetes on a Cloud Provider

This section outlines the steps to deploy a Kubernetes cluster on a cloud platform and create a deployment.

![Untitled 1 46.png](../../../../Images/Untitled%201%2046.png)

### Step 1: Create a Kubernetes Cluster

1. Choose a cloud provider:
    - Amazon Web Services (AWS)
    - Google Cloud Platform (GCP)
    - Digital Ocean
    - Vultr
2. Navigate to the Kubernetes or container service section of your chosen provider.
3. Create a new Kubernetes cluster:
    - Specify the desired number of nodes
    - Choose the node types/sizes
    - Configure networking options
    - Set up access controls

### Step 2: Configure kubectl

1. After cluster creation, download the credentials file from your cloud provider's dashboard.
2. Replace the contents of your local `~/.kube/config` file with the downloaded credentials:
    
    ```Shell
    mv ~/Downloads/kubeconfig ~/.kube/config
    ```
    

### Step 3: Create a Deployment

1. Create a file named `deployment.yml` with the following content:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx2:latest
        ports:
        - containerPort: 80
```

1. Apply the deployment:

```Shell
kubectl apply -f deployment.yml
```

### Key Points

1. **Cloud Provider Selection**: Choose a provider that best fits your needs in terms of pricing, features, and geographical availability.
2. **Cluster Configuration**: Pay attention to node sizes and counts to ensure your cluster meets your application's resource requirements.
3. **Security**: Ensure your cluster is properly secured, including network policies and access controls.
4. **Credentials Management**: Keep your kubeconfig file secure, as it contains sensitive information for cluster access.
5. **Image Availability**: Ensure the container image specified in your deployment (in this case, `nginx2:latest`) is available and accessible to your cluster.
6. **Monitoring**: Set up monitoring and logging solutions to keep track of your cluster's health and performance.

Remember, running Kubernetes in the cloud offers scalability and managed services, but also requires careful consideration of costs and resource management.

  

  

# Services in Kubernetes

Services in Kubernetes provide a way to expose your application to network traffic, either within the cluster or externally. Let's explore two types of services: NodePort and LoadBalancer.

### NodePort Service

NodePort exposes the service on each Node's IP at a static port.

1. Create a file named `service.yml` for NodePort:

```YAML
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30007  # This port can be any valid port within the NodePort range
  type: NodePort
```

1. Apply the service:

```Shell
kubectl apply -f service.yml
```

1. Access the service:
    - For local clusters (e.g., Kind): `http://localhost:30007/`
    - For cloud providers: Use the node's public IP, e.g., `http://<node-ip>:30007/`

Note: This will only work if you've started your Kind cluster with the config from the previous section that maps the ports.

![Untitled 2 34.png](../../../../Images/Untitled%202%2034.png)

### LoadBalancer Service

The LoadBalancer service type works with cloud providers to create an external load balancer that routes traffic to the service.

1. Modify `service.yml` for LoadBalancer:

```YAML
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

1. Apply the updated service:

```Shell
kubectl apply -f service.yml
```

1. Check the service status:

```Shell
kubectl get services
```

Look for the EXTERNAL-IP column. It may take a few minutes to provision.

1. Access the service using the external IP provided by the cloud provider.

### Key Points

1. **NodePort**:
    - Makes a service accessible on a static port on each Node.
    - Useful for development and when you have direct access to node IPs.
    - Limited to ports 30000-32767 by default.
2. **LoadBalancer**:
    - Creates an external load balancer in cloud providers.
    - Automatically creates a NodePort and ClusterIP service to which it routes.
    - Provides a single point of contact for external traffic.
    - Only works fully on cloud providers that support external load balancers.
3. **Selector**:  
    Both service types use  
    `selector` to determine which pods to route traffic to.
4. **Cloud Provider Integration**:  
    LoadBalancer services integrate with your cloud provider's load balancing service, which may incur additional costs.  
    
5. **Local vs. Cloud**:
    - NodePort works similarly in both local and cloud environments.
    - LoadBalancer functionality is limited in local environments like Kind or Minikube.
6. **Security Considerations**:  
    When exposing services, ensure proper security measures are in place, such as firewalls and network policies.  
    

> Remember, the choice between NodePort and LoadBalancer often depends on your specific use case and environment. NodePort is often used for development or internal services, while LoadBalancer is typically used for production services that need to be accessible from the internet.

  

  

  

# Downsides of Services

1. **Scaling to Multiple Apps**:
    
    - Each app requires its own service, leading to multiple load balancers.
    - No centralized traffic management or path-based routing.
    - Cloud providers often limit the number of load balancers you can create.
    
    ![Untitled 3 30.png](../../../../Images/Untitled%203%2030.png)
    
2. **Certificate Management**:
    
    - Certificates for load balancers must be managed outside the cluster.
    - Manual creation and updating of certificates.
    - Separate certificates required for each service/route.
    
    ![Untitled 4 27.png](../../../../Images/Untitled%204%2027.png)
    
3. **Lack of Centralized Rate Limiting**:
    
    - No unified rate limiting across all services.
    - Each load balancer may have its own rate limits, but there's no global control.
    
    ![Untitled 5 22.png](../../../../Images/Untitled%205%2022.png)
    

  

### Practical Demonstration

Let's create two deployments (NGINX and Apache) with their respective LoadBalancer services.

1. Create a file named `manifest.yml` with the following content:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: apache-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: apache
  template:
    metadata:
      labels:
        app: apache
    spec:
      containers:
      - name: my-apache-site
        image: httpd:2.4
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
---
apiVersion: v1
kind: Service
metadata:
  name: apache-service
spec:
  selector:
    app: apache
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

1. Apply the manifest:

```Shell
kubectl apply -f manifest.yml
```

1. Verify the creation of services:

```Shell
kubectl get services
```

You should see two LoadBalancer services created, one for NGINX and one for Apache.

### Key Observations

1. **Multiple Load Balancers**: This setup creates two separate load balancers, one for each service.
2. **Resource Utilization**: Each load balancer consumes cloud resources and may incur additional costs.
3. **Separate Management**: Each service and its associated load balancer need to be managed independently.
4. **No Shared Routing**: There's no built-in way to route traffic based on paths or other rules between these services.
5. **Certificate Challenges**: If HTTPS is required, you'd need to manage certificates for each load balancer separately.

### Potential Solutions

To address these limitations, Kubernetes offers more advanced resources:

1. **Ingress**: Provides a way to manage external access to services, typically HTTP, allowing path-based routing and SSL termination.
2. **Ingress Controllers**: Implement the Ingress resource, offering more advanced routing capabilities.
3. **Service Mesh**: Platforms like Istio or Linkerd can provide advanced traffic management, security, and observability features.
4. **Custom Resource Definitions (CRDs)**: Allow for extending Kubernetes API to define resources that can manage complex routing and certificate management.

These solutions can help centralize traffic management, simplify certificate handling, and provide more granular control over routing and rate limiting across multiple services.

  

  

  

# Ingress and Ingress Controller

Ingress is a crucial Kubernetes resource that manages external access to services within a cluster, primarily for HTTP traffic. Let's explore the key aspects of Ingress and Ingress Controllers:

![Untitled 6 20.png](../../../../Images/Untitled%206%2020.png)

## Ingress

1. **Definition**:
    - An API object that manages external access to services in a cluster.
    - Typically used for HTTP traffic.
2. **Key Features**:
    - Provides load balancing
    - Offers SSL/TLS termination
    - Enables name-based virtual hosting
3. **Functionality**:
    - Acts as an entry point for your cluster
    - Routes traffic to different services based on rules
4. **Limitations**:
    - Does not expose arbitrary ports or protocols
    - Limited to HTTP and HTTPS traffic

### Important Note:

For exposing services other than HTTP/HTTPS to the internet, you typically use:

- `Service.Type=NodePort`
- `Service.Type=LoadBalancer`

## Ingress Controller

1. **Purpose**:
    - Implements the Ingress resource
    - Responsible for fulfilling the Ingress rules
2. **Types**:
    - Various implementations available (e.g., NGINX, Traefik, HAProxy)
    - Cloud providers often have their own implementations
3. **Functionality**:
    - Watches for Ingress resources and updates
    - Configures the underlying load balancer or proxy

### Key Benefits of Using Ingress

1. **Centralized Routing**: Manage multiple services through a single entry point
2. **SSL/TLS Termination**: Handle HTTPS traffic and certificate management
3. **Name-based Virtual Hosting**: Route to different services based on the domain name
4. **Path-based Routing**: Direct traffic to different services based on URL paths
5. **Reduced Cost**: Can reduce the number of load balancers needed

## Considerations

1. **Ingress Controller Selection**: Choose based on your specific needs and environment
2. **Configuration Complexity**: More complex to set up than simple Service exposures
3. **Security**: Properly configure to avoid exposing sensitive services
4. **Monitoring**: Important to monitor Ingress performance and behavior

  

> Ingress provides a powerful way to manage external access to your Kubernetes services, offering more flexibility and features compared to simple NodePort or LoadBalancer service types. However, it requires careful configuration and management to ensure secure and efficient traffic routing.

  

  

# Ingress Controllers

![Untitled 7 18.png](../../../../Images/Untitled%207%2018.png)

1. **Control Plane Components**:
    - The Kubernetes control plane includes a controller manager that runs various controllers.
    - Examples include ReplicaSet controller and Deployment controller.
2. **Manual Installation Required**:
    - Ingress controllers are not included by default in Kubernetes.
    - They need to be installed manually to add Ingress functionality to a cluster.
3. **Popular Ingress Controllers**:
    - NGINX Ingress Controller: Works with the NGINX webserver as a proxy.
    - HAProxy Ingress: An Ingress controller for HAProxy.
    - Traefik Kubernetes Ingress provider: An Ingress controller for the Traefik proxy.
4. **Variety of Options**:
    - There are many other Ingress controllers available for Kubernetes.
    - A full list can be found in the Kubernetes documentation.
5. **Purpose**:
    - Ingress controllers implement the Ingress resource in Kubernetes.
    - They manage external access to services within a cluster, typically for HTTP traffic.
6. **Flexibility**:
    - Different Ingress controllers can be chosen based on specific needs and preferences.
    - They offer various features and integration options with different proxy technologies.
7. **Integration with Kubernetes**:
    - While not part of the core Kubernetes components, Ingress controllers integrate closely with the Kubernetes API and resources.
8. **Configuration**:
    - After installation, Ingress controllers typically require configuration to work with the cluster's specific setup and requirements.

This information highlights the importance of Ingress controllers in extending Kubernetes' networking capabilities, particularly for managing external access to services within the cluster.

  

  

  

# Kubernetes Namespaces

Namespaces in Kubernetes provide a mechanism for isolating groups of resources within a single cluster. They are particularly useful in environments with multiple users, teams, or projects. Let's explore how to work with namespaces:

### Understanding Namespaces

1. **Purpose**:
    - Divide cluster resources between multiple users, teams, or projects.
    - Useful for separating environments (e.g., development, staging, production).
2. **Default Behavior**:
    - When you run `kubectl get pods`, it shows pods in the default namespace.

### Working with Namespaces

1. **Creating a New Namespace**:
    
    ```Shell
    kubectl create namespace backend-team
    ```
    
2. **Listing All Namespaces**:
    
    ```Shell
    kubectl get namespaces
    ```
    
3. **Getting Pods in a Specific Namespace**:
    
    ```Shell
    kubectl get pods -n my-namespace
    ```
    

### Creating Resources in a Namespace

1. **Deployment Manifest with Namespace**:  
    Create a file  
    `deployment-ns.yml`:
    
    ```YAML
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-deployment
      namespace: backend-team
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx:latest
            ports:
            - containerPort: 80
    ```
    
2. **Applying the Manifest**:
    
    ```Shell
    kubectl apply -f deployment-ns.yml
    ```
    
3. **Checking Deployments in the Namespace**:
    
    ```Shell
    kubectl get deployment -n backend-team
    ```
    
4. **Checking Pods in the Namespace**:
    
    ```Shell
    kubectl get pods -n backend-team
    ```
    

### Changing Default Namespace

1. **Set Default Namespace for Current Context**:
    
    ```Shell
    kubectl config set-context --current --namespace=backend-team
    ```
    
2. **Verify (now** `**kubectl get pods**` **will show pods in backend-team namespace)**:
    
    ```Shell
    kubectl get pods
    ```
    
3. **Reverting to Default Namespace**:
    
    ```Shell
    kubectl config set-context --current --namespace=default
    ```
    

### Key Points

1. **Isolation**: Namespaces provide a scope for names, allowing you to use the same resource names in different namespaces.
2. **Resource Quotas**: You can use namespaces to divide cluster resources between users or teams.
3. **Access Control**: Namespaces can be used with role-based access control (RBAC) to restrict access to resources.
4. **Default Namespace**: If not specified, operations are performed in the 'default' namespace.
5. **Cross-Namespace Communication**: Services in one namespace can communicate with services in another namespace using fully qualified domain names.
6. **Not All Objects are Namespaced**: Some Kubernetes resources (like nodes) are not in any namespace.

> Namespaces are a powerful feature for organizing and isolating resources within a Kubernetes cluster, especially useful in multi-tenant environments or for separating different stages of development.

  

  

# Installing the NGINX Ingress Controller

![Untitled 8 15.png](../../../../Images/Untitled%208%2015.png)

The detailed steps for installation of the NGINX Ingress Controller using Helm are as follows:

### 1. Install Helm

Helm is a package manager for Kubernetes. If you haven't installed it yet:

- Visit the official Helm website: [https://helm.sh/](https://helm.sh/)
- Follow the installation instructions: [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)

### 2. Add and Update the ingress-nginx Repository

```Shell
helm repo add ingress-nginx <https://kubernetes.github.io/ingress-nginx>
helm repo update
```

### 3. Install NGINX Ingress Controller

```Shell
helm install nginx-ingress ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace
```

This command:

- Installs the NGINX Ingress Controller
- Creates a new namespace called `ingress-nginx`
- Names the release `nginx-ingress`

### 4. Verify the Installation

Check if the Ingress Controller pods are running:

```Shell
kubectl get pods -n ingress-nginx
```

You should see at least one pod running for the NGINX Ingress Controller.

### 5. Check the Created LoadBalancer Service

Helm automatically creates a LoadBalancer service for the Ingress Controller:

```Shell
kubectl get services --all-namespaces
```

Look for a service in the `ingress-nginx` namespace with type `LoadBalancer`.

### Key Points

1. **Default LoadBalancer**: The Helm chart automatically creates a LoadBalancer service, which routes all incoming traffic to the NGINX Ingress Controller pod(s).
2. **Ingress Controller Pod**: This pod is responsible for routing traffic based on Ingress rules you'll define later.
3. **Namespace Isolation**: The Ingress Controller is installed in its own namespace (`ingress-nginx`) for better resource management and isolation.
4. **Cloud Integration**: On cloud providers, the LoadBalancer service will provision an external IP or hostname for accessing your cluster.
5. **Next Steps**: With the Ingress Controller installed, you're now ready to define Ingress resources to route traffic to your services.
6. **Customization**: The Helm installation can be customized with various options. Refer to the NGINX Ingress Controller documentation for advanced configurations.
7. **Monitoring**: It's important to monitor the Ingress Controller pods and the associated LoadBalancer service for proper functioning.

  

  

# Setting Up Ingress Routing

Ingress routing in Kubernetes is a mechanism for managing external access to services within a cluster. This comprehensive guide walks through the process of setting up Ingress routing for NGINX and Apache services in a Kubernetes cluster. Let's break it down step-by-step:

![Untitled 9 11.png](../../../../Images/Untitled%209%2011.png)

### 1. Clean Up Existing Resources

First, remove any existing deployments and services:

```Shell
kubectl get deployments
kubectl delete deployment <deployment_name>

kubectl get services
kubectl delete service <service_name>
```

Note: Don't delete the default Kubernetes service.

### 2. Create Combined Manifest

Create a file named `complete.yml` with the following content:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: default
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: default
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: apache-deployment
  namespace: default
spec:
  replicas: 2
  selector:
    matchLabels:
      app: apache
  template:
    metadata:
      labels:
        app: apache
    spec:
      containers:
      - name: my-apache-site
        image: httpd:2.4
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: apache-service
  namespace: default
spec:
  selector:
    app: apache
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: web-apps-ingress
  namespace: default
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - host: your-domain.com
    http:
      paths:
      - path: /nginx
        pathType: Prefix
        backend:
          service:
            name: nginx-service
            port:
              number: 80
      - path: /apache
        pathType: Prefix
        backend:
          service:
            name: apache-service
            port:
              number: 80
```

### 3. Apply the Manifest

Apply the combined manifest:

```Shell
kubectl apply -f complete.yml
```

### 4. Update Local Hosts File

Add an entry to your `/etc/hosts` file:

```Plain
65.20.84.86    your-domain.com
```

Replace `65.20.84.86` with the actual IP of your Ingress Controller's LoadBalancer service.

### 5. Test the Setup

Visit `your-domain.com/apache` and `your-domain.com/nginx` in your web browser.

### Key Components

1. **NGINX Deployment and Service**: Deploys NGINX pods and creates a ClusterIP service for them.
2. **Apache Deployment and Service**: Deploys Apache pods and creates a ClusterIP service for them.
3. **Ingress Resource**:
    - Defines routing rules for incoming HTTP traffic.
    - Routes `/nginx` to the NGINX service and `/apache` to the Apache service.
    - Uses `your-domain.com` as the host.

### Important Notes

1. **ClusterIP Services**: Both services are of type ClusterIP, making them only internally accessible.
2. **Ingress Controller**: Assumes you have already installed the NGINX Ingress Controller.
3. **Rewrite Annotation**: The `nginx.ingress.kubernetes.io/rewrite-target: /` annotation ensures proper URL rewriting.
4. **IngressClassName**: Specifies `nginx` as the Ingress class, linking it to the NGINX Ingress Controller.
5. **Host-Based Routing**: The Ingress is configured for a specific domain (`your-domain.com`).
6. **Path-Based Routing**: Different paths (`/nginx` and `/apache`) route to different services.
7. **Local Testing**: Modifying the hosts file allows for local testing without actual DNS configuration.

### Conclusion

This setup demonstrates the power of Kubernetes Ingress:

- Single entry point for multiple services
- Path-based and host-based routing
- Simplified external access management

By using Ingress, you can efficiently manage external access to your services, reducing the need for multiple LoadBalancer services and providing more flexible routing options.

  

  

# Trying Traefik's Ingress Controller

Traefik's Ingress Controller is a Kubernetes component that manages external access to services within a cluster. Traefik's Ingress Controller offers a flexible and powerful solution for managing ingress traffic in Kubernetes environments, with features that make it suitable for both development and production use cases. Here are the key points about Traefik's Ingress Controller:  
  

### 1. Install Traefik Ingress Controller

Use Helm to install Traefik:

```Shell
helm repo add traefik <https://helm.traefik.io/traefik>
helm repo update
helm install traefik traefik/traefik --namespace traefik --create-namespace
```

### 2. Verify Installation

Check if the IngressClass for Traefik is created:

```Shell
kubectl get IngressClass
```

Verify that a LoadBalancer service is created for Traefik:

```Shell
kubectl get svc -n traefik
```

### 3. Create Traefik Ingress Resource

Create a file named `traefik.yml` with the following content:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: traefik-web-apps-ingress
  namespace: default
spec:
  ingressClassName: traefik
  rules:
  - host: traefik-domain.com
    http:
      paths:
      - path: /nginx
        pathType: Prefix
        backend:
          service:
            name: nginx-service
            port:
              number: 80
      - path: /apache
        pathType: Prefix
        backend:
          service:
            name: apache-service
            port:
              number: 80
```

Apply this configuration:

```Shell
kubectl apply -f traefik.yml
```

### 4. Update Local Hosts File

Add an entry to your `/etc/hosts` file:

```Plain
65.20.90.183    traefik-domain.com
```

Replace `65.20.90.183` with the actual IP of your Traefik LoadBalancer service.

### 5. Test the Setup

Try accessing:

- `traefik-domain.com/nginx`
- `traefik-domain.com/apache`

### Issue Identification

You might notice that you're not seeing the expected content when accessing these URLs. The problem is likely due to path rewriting not being configured in the Traefik Ingress resource.

![Untitled 10 10.png](../../../../Images/Untitled%2010%2010.png)

### Assignment: Path Rewriting with Traefik

To fix this issue, you need to configure path rewriting for Traefik. Here's a hint on how to do it:

1. Traefik uses middleware for path manipulation.
2. You'll need to create a Middleware resource for path rewriting.
3. Then, annotate your Ingress resource to use this middleware.

Try to implement this solution. Here's a starting point:

```YAML
apiVersion: traefik.containo.us/v1alpha1
kind: Middleware
metadata:
  name: strip-prefix
spec:
  stripPrefix:
    prefixes:
      - /nginx
      - /apache

---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: traefik-web-apps-ingress
  annotations:
    traefik.ingress.kubernetes.io/router.middlewares: default-strip-prefix@kubernetescrd
  # ... rest of your Ingress spec
```

### Key Points

1. **Traefik vs NGINX**: Traefik offers a different approach to Ingress control compared to NGINX.
2. **IngressClass**: Ensure you're using the correct IngressClass (`traefik` in this case).
3. **Path Rewriting**: Unlike NGINX, Traefik requires explicit configuration for path rewriting.
4. **Middleware**: Traefik uses the concept of middleware for manipulating requests.
5. **Annotations**: Traefik often uses annotations for advanced configurations.

By completing this assignment, you'll gain a deeper understanding of how Traefik works as an Ingress Controller and how it differs from NGINX in terms of configuration and features.

  

  

# Secrets and ConfigMaps

This section introduces two important Kubernetes resources for managing application configuration: ConfigMaps and Secrets. These resources allow you to decouple configuration details from container images and pods, following best practices for Kubernetes deployments.

![Untitled 11 8.png](../../../../Images/Untitled%2011%208.png)

### Kubernetes Configuration Best Practices

1. **Use Deployments**: Always create Deployments rather than standalone pods.
2. **YAML Over JSON**: Write configuration files using YAML instead of JSON for better readability.
3. **Version Control**: Store configuration files in version control before applying them to the cluster.
4. **Externalize Configuration**: Use ConfigMaps and Secrets to store configuration outside of container images.

![Untitled 12 7.png](../../../../Images/Untitled%2012%207.png)

### ConfigMaps and Secrets

Both ConfigMaps and Secrets are used to store configuration data, but they serve different purposes:

1. **ConfigMaps**:
    - Store non-sensitive configuration data.
    - Can be used for environment variables, command-line arguments, or configuration files.
    - Data is stored as plain text.
2. **Secrets**:
    - Store sensitive information like passwords, tokens, or keys.
    - Similar to ConfigMaps but intended for confidential data.
    - Data is base64 encoded (but not encrypted by default).

### Key Rule: Externalize Secrets

A crucial rule of thumb in Kubernetes:

- Don't bake application secrets into your Docker images.
- Instead, pass them as environment variables when starting containers.

### Using ConfigMaps and Secrets

1. **As Environment Variables**:
    - Inject configuration data directly into container environments.
2. **As Files**:
    - Mount ConfigMaps or Secrets as volumes in pods.
3. **As Command-line Arguments**:
    - Use data to construct container command-line args.

### Example: Creating and Using a ConfigMap

```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: blue
  APP_MODE: prod
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  template:
    spec:
      containers:
      - name: my-app
        image: my-app:v1
        envFrom:
        - configMapRef:
            name: app-config
```

### Example: Creating and Using a Secret

```YAML
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  DB_PASSWORD: base64encodedpassword
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  template:
    spec:
      containers:
      - name: my-app
        image: my-app:v1
        env:
        - name: DATABASE_PASSWORD
          valueFrom:
            secretKeyRef:
              name: app-secret
              key: DB_PASSWORD
```

### Benefits of Using ConfigMaps and Secrets

1. **Separation of Concerns**: Keep application code separate from configuration.
2. **Flexibility**: Easily update configuration without changing container images.
3. **Security**: Better management of sensitive data.
4. **Reusability**: Use the same container image with different configurations.

  

> By leveraging ConfigMaps and Secrets, you can create more secure, flexible, and maintainable Kubernetes deployments, adhering to best practices for configuration management in containerized environments.

  

  

# ConfigMaps

This section covers the creation and usage of ConfigMaps in Kubernetes, demonstrating how to decouple configuration from application code.

### What is a ConfigMap?

A ConfigMap is an API object used to store non-confidential data in key-value pairs. It allows you to decouple environment-specific configuration from container images, enhancing application portability.

### Creating a ConfigMap

1. Create a file named `cm.yml`:

```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: ecom-backend-config
data:
  database_url: "mysql://ecom-db:3306/shop"
  cache_size: "1000"
  payment_gateway_url: "<https://payment-gateway.example.com>"
  max_cart_items: "50"
  session_timeout: "3600"
```

1. Apply the ConfigMap:

```Shell
kubectl apply -f cm.yml
```

1. Verify the ConfigMap:

```Shell
kubectl describe configmap ecom-backend-config
```

### Creating an Express App with Environment Variables

1. Create an Express app that exposes environment variables.
2. Deploy the app to Docker Hub: [100xdevs/env-backend](https://hub.docker.com/repository/docker/100xdevs/env-backend/general)
3. Test locally with Docker:

```Shell
docker run -p 3003:3000 -e DATABASE_URL=asd 100xdevs/env-backend
```

![Untitled 13 3.png](../../../../Images/Untitled%2013%203.png)

### Deploying the Express App in Kubernetes

1. Create a file named `express-app.yml`:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ecom-backend-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ecom-backend
  template:
    metadata:
      labels:
        app: ecom-backend
    spec:
      containers:
      - name: ecom-backend
        image: 100xdevs/env-backend
        ports:
        - containerPort: 3000
        env:
        - name: DATABASE_URL
          valueFrom:
            configMapKeyRef:
              name: ecom-backend-config
              key: database_url
        - name: CACHE_SIZE
          valueFrom:
            configMapKeyRef:
              name: ecom-backend-config
              key: cache_size
        - name: PAYMENT_GATEWAY_URL
          valueFrom:
            configMapKeyRef:
              name: ecom-backend-config
              key: payment_gateway_url
        - name: MAX_CART_ITEMS
          valueFrom:
            configMapKeyRef:
              name: ecom-backend-config
              key: max_cart_items
        - name: SESSION_TIMEOUT
          valueFrom:
            configMapKeyRef:
              name: ecom-backend-config
              key: session_timeout
```

1. Apply the Deployment:

```Shell
kubectl apply -f express-app.yml
```

![Untitled 14 2.png](../../../../Images/Untitled%2014%202.png)

### Creating a Service for the Express App

1. Create a file named `express-service.yml`:

```YAML
apiVersion: v1
kind: Service
metadata:
  name: ecom-backend-service
spec:
  type: NodePort
  selector:
    app: ecom-backend
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 30007
```

1. Apply the Service:

```Shell
kubectl apply -f express-service.yml
```

### Accessing the Application

Visit the application using the NodePort (30007) on any of your cluster's node IPs.

### Key Points

1. **ConfigMap Usage**: ConfigMaps store configuration data separately from application code.
2. **Environment Variables**: The Deployment uses `configMapKeyRef` to inject ConfigMap values as environment variables.
3. **Portability**: This approach allows for easy configuration changes without modifying the container image.
4. **NodePort Service**: The NodePort service makes the application accessible outside the cluster.
5. **Separation of Concerns**: Configuration, application code, and deployment specifications are all separated.

  

> This setup demonstrates how to effectively use ConfigMaps to manage application configuration in Kubernetes, promoting better practices in configuration management and application deployment.