In this lecture, Harkirat explores data persistence and scaling in containerized environments. He begins with volumes in Docker, then transitions to Kubernetes, covering both ephemeral and persistent volumes. The lecture delves into static persistent volumes and automated PV creation, demonstrating how to manage stateful applications effectively.

  

  

Volumes in Docker

Pretext: Sample Application

Key Points:

Key Takeaways:

Volumes in Kubernetes

Why Volumes are Needed

Types of Volumes

Key Concepts

Ephemeral Volumes

Setup Example

Key Points

Persistent Volumes

Key Concepts

Visualization

Key Points

Use Cases

Best Practices

Static Persistent Volumes

Setting up NFS Server

Creating PV and PVC

Creating a Pod with PV

Testing Persistence

Key Points

Best Practices

Automative PV Creation

Horizontal Pod Autoscaler

  

# Volumes in Docker

![Untitled 56.png](../../../../Images/Untitled%2056.png)

### Pretext: Sample Application

A Node.js application that periodically writes random data to a file is used as an example. The Docker image for this app is available at `100xdevs/write-random`.

### Key Points:

1. **Ephemeral Storage in Docker**:
    - By default, data in Docker containers is ephemeral.
    - Data is lost when the container is stopped or removed.
2. **Running the Sample Container**:
    
    ```Shell
    docker run 100xdevs/write-random
    ```
    
3. **Inspecting Container Data**:
    
    ```Shell
    docker exec -it container_id /bin/bash
    cat randomData.txt
    ```
    
4. **Volumes in Docker**:
    - Used to persist data across container stops and starts.
    - Two main types: Bind Mounts and Volume Mounts.
5. **Bind Mounts**:
    - Maps a host machine directory to a container directory.
    - Example:
        
        ```Shell
        docker run -v /Users/harkiratsingh/Projects/100x/mount:/usr/src/app/generated 100xdevs/write-random
        ```
        
6. **Volume Mounts**:
    - Uses Docker-managed volumes for data persistence.
    - Creating a volume:
        
        ```Shell
        docker volume create hello
        ```
        
    - Using the volume:
        
        ```Shell
        docker run -v hello:/usr/src/app/generated 100xdevs/write-random
        ```
        
7. **Data Persistence**:
    - With both bind mounts and volume mounts, data persists even if the container is stopped.

### Key Takeaways:

1. Docker containers by default use ephemeral storage.
2. Volumes provide a way to persist data beyond the container's lifecycle.
3. Bind mounts directly map host directories to container directories.
4. Volume mounts use Docker-managed volumes for more portable and flexible data storage.
5. Both methods ensure data persistence across container restarts or removals.

Understanding volumes is crucial for managing stateful applications in Docker environments, allowing for data persistence and easier management of application state.

  

  

# Volumes in Kubernetes

Volumes in Kubernetes are directories, potentially containing data, that are accessible to containers within a pod. They serve several important purposes in container orchestration.

![Untitled 1 47.png](../../../../Images/Untitled%201%2047.png)

### Why Volumes are Needed

1. **Inter-Container Data Sharing**: Allows containers in the same pod to share data and filesystems.
2. **Data Persistence**: Enables data to persist even when containers restart, crucial for databases and stateful applications.
3. **Temporary Storage**: Provides extra space for execution needs like caching, without requiring persistence.

  

![Untitled 2 35.png](../../../../Images/Untitled%202%2035.png)

### Types of Volumes

1. **Ephemeral Volumes**
    - Temporary storage shared among containers in a pod
    - Lifecycle tied to the pod (destroyed when pod is deleted)
    - Examples:
        - ConfigMap
        - Secret
        - emptyDir
2. **Persistent Volumes (PV)**
    - Storage in the cluster provisioned by an administrator or dynamically via Storage Classes
    - Lifecycle independent of any individual pod
    - Can use various storage backends (NFS, iSCSI, cloud-provider storage)
3. **Persistent Volume Claims (PVC)**
    - User requests for storage
    - Similar to how pods consume node resources, PVCs consume PV resources
    - Can request specific size and access modes

![Untitled 3 31.png](../../../../Images/Untitled%203%2031.png)

### Key Concepts

- Volumes solve the problem of data persistence in containerized environments
- They enable data sharing between containers and across pod restarts
- Kubernetes supports a wide variety of volume types to suit different needs
- PVs and PVCs provide a way to abstract storage details from pod specifications

Understanding and effectively using volumes is crucial for managing stateful applications and ensuring data persistence in Kubernetes environments.

  

  

# Ephemeral Volumes

Ephemeral volumes allow containers in the same pod to share data, but the data is lost when the pod is terminated.

![Untitled 4 28.png](../../../../Images/Untitled%204%2028.png)

### Setup Example

1. **Create a Manifest (kube.yml)**:
    
    ```YAML
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: shared-volume-deployment
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: shared-volume-app
      template:
        metadata:
          labels:
            app: shared-volume-app
        spec:
          containers:
          - name: writer
            image: busybox
            command: ["/bin/sh", "-c", "echo 'Hello from Writer Pod' > /data/hello.txt; sleep 3600"]
            volumeMounts:
            - name: shared-data
              mountPath: /data
          - name: reader
            image: busybox
            command: ["/bin/sh", "-c", "cat /data/hello.txt; sleep 3600"]
            volumeMounts:
            - name: shared-data
              mountPath: /data
          volumes:
          - name: shared-data
            emptyDir: {}
    ```
    
2. **Apply the Manifest**:
    
    ```Shell
    kubectl apply -f kube.yml
    ```
    
3. **Verify Data Sharing**:
    
    ```Shell
    kubectl exec -it shared-volume-deployment-74d67d6567-tcdsl --container reader sh
    ```
    

### Key Points

1. **emptyDir Volume**:
    - Type of ephemeral volume used in this example.
    - Created when a Pod is assigned to a node, exists as long as that Pod is running on that node.
    - Initially empty.
2. **Data Sharing**:
    - Both containers (`writer` and `reader`) mount the same volume at `/data`.
    - `writer` container writes to the volume, `reader` container can read from it.
3. **Lifecycle**:
    - Data in the volume persists across container restarts within the pod.
    - Data is lost when the pod is deleted or rescheduled to a different node.
4. **Use Cases**:
    - Temporary scratch space.
    - Sharing data between containers in a pod.
    - Caching.
5. **Performance**:
    - Typically faster than network-based storage.
    - Resides on the node's filesystem.
6. **Limitations**:
    - Not suitable for persistent data storage.
    - Data is lost if the pod is removed from the node.

  

# Persistent Volumes

Persistent Volumes provide a powerful abstraction for managing storage in Kubernetes. They allow for efficient use of storage resources, enable data persistence across pod lifecycles, and support both static and dynamic provisioning to meet various application needs.

![Untitled 5 23.png](../../../../Images/Untitled%205%2023.png)

### Key Concepts

1. **Persistent Volumes (PVs)**:
    - Pieces of storage in the cluster
    - Provisioned by an administrator or dynamically using Storage Classes
    - Exist independently of any pod
2. **Persistent Volume Claims (PVCs)**:
    - Requests for storage by users
    - Pods use PVCs to claim PV resources
3. **Storage Provisioning**:
    - Static: Admin pre-creates PVs
    - Dynamic: PVs are created on-demand using Storage Classes

### Visualization

The provided image illustrates:

- Kubernetes cluster with nodes for running pods
- Persistent Volumes as a separate resource pool
- Pods claiming storage from PVs

### Key Points

1. **Separation of Concerns**:
    - PVs separate storage provisioning from pod deployment
    - Allows for more flexible and scalable storage management
2. **Lifecycle Independence**:
    - PVs have a lifecycle independent of pods
    - Data persists even when pods are deleted or rescheduled
3. **Storage Classes**:
    - Define different types of storage (e.g., SSD, HDD)
    - Enable dynamic provisioning of PVs
4. **Access Modes**:
    - ReadWriteOnce (RWO): Read-write by a single node
    - ReadOnlyMany (ROX): Read-only by many nodes
    - ReadWriteMany (RWX): Read-write by many nodes
5. **Reclaim Policies**:
    - Retain: Keep data for manual cleanup
    - Delete: Delete the volume and its data
    - Recycle: Basic scrub (deprecated)

### Use Cases

1. Databases requiring persistent storage
2. Shared file systems across multiple pods
3. Long-term data storage in stateful applications

### Best Practices

1. Use Storage Classes for dynamic provisioning where possible
2. Implement appropriate backup and disaster recovery strategies
3. Monitor PV usage and capacity
4. Use appropriate access modes and reclaim policies

  

  

  

# Static Persistent Volumes

### Setting up NFS Server

1. **NFS Server Setup (on AWS)**:  
    Note: Ensure port 2049 is open on your machine.  
    
    ```YAML
    version: '3.7'
    services:
      nfs-server:
        image: itsthenetwork/nfs-server-alpine:latest
        container_name: nfs-server
        privileged: true
        environment:
          SHARED_DIRECTORY: /exports
        volumes:
          - ./data:/exports:rw
        ports:
          - "2049:2049"
        restart: unless-stopped
    ```
    

### Creating PV and PVC

1. **Create PV and PVC**:
    
    ```YAML
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: nfs-pv
    spec:
      capacity:
        storage: 10Gi
      accessModes:
        - ReadWriteMany
      storageClassName: nfs
      nfs:
        path: /exports
        server: 52.66.197.168
    ---
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: nfs-pvc
    spec:
      accessModes:
        - ReadWriteMany
      resources:
        requests:
          storage: 10Gi
      storageClassName: nfs
    ```
    

### Creating a Pod with PV

1. **Create Pod Using PVC**:
    
    ```YAML
    apiVersion: v1
    kind: Pod
    metadata:
      name: mongo-pod
    spec:
      containers:
      - name: mongo
        image: mongo:4.4
        command: ["mongod", "--bind_ip_all"]
        ports:
        - containerPort: 27017
        volumeMounts:
        - mountPath: "/data/db"
          name: nfs-volume
      volumes:
      - name: nfs-volume
        persistentVolumeClaim:
          claimName: nfs-pvc
    ```
    

### Testing Persistence

1. **Insert Data**:
    
    ```Shell
    kubectl exec -it mongo-pod -- mongo
    use mydb
    db.mycollection.insert({ name: "Test", value: "This is a test" })
    exit
    ```
    
2. **Delete and Recreate Pod**:
    
    ```Shell
    kubectl delete pod mongo-pod
    kubectl apply -f mongo.yml
    ```
    
3. **Verify Data Persistence**:
    
    ```Shell
    kubectl exec -it mongo-pod -- mongo
    use mydb
    db.mycollection.find()
    ```
    

![Untitled 6 21.png](../../../../Images/Untitled%206%2021.png)

  

### Key Points

1. **NFS as PV**: NFS is used as an example of a network storage solution for PVs.
2. **Static Provisioning**: PV is manually created before the PVC.
3. **PV and PVC Binding**: PVC binds to the PV based on storage class and access modes.
4. **Pod Volume Mount**: The pod uses the PVC to mount the volume.
5. **Data Persistence**: Data persists even when the pod is deleted and recreated.

### Best Practices

1. Ensure proper security measures for NFS server access.
2. Use appropriate storage classes for different types of applications.
3. Monitor PV usage and implement proper capacity planning.
4. Implement backup strategies for data stored in PVs.

  

> Static Persistent Volumes provide a way to use pre-provisioned storage in Kubernetes. This approach is useful when you have existing storage infrastructure or specific storage requirements. It allows for data persistence across pod lifecycles, which is crucial for stateful applications like databases.

  

  

# Automative PV Creation

Here's a summary of how to set up automatic Persistent Volume (PV) creation in Kubernetes using Vultr's block storage.

1. Create a Persistent Volume Claim (PVC):
    - Use the `vultr-block-storage-hdd` storage class
    - Request 40Gi of storage
    - Use ReadWriteOnce access mode
2. Create a Pod that uses the PVC:
    - Use a MongoDB container
    - Mount the PVC to `/data/db` in the container
3. Apply the configurations and verify:
    - Check created PV, PVC, and Pod
4. Test data persistence:
    - Insert data into MongoDB
    - Delete and recreate the Pod
    - Verify that the data persists

Key steps:

1. Create PVC:

```YAML
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: csi-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 40Gi
  storageClassName: vultr-block-storage-hdd
```

1. Create Pod:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: mongo-pod
spec:
  containers:
  - name: mongo
    image: mongo:4.4
    command: ["mongod", "--bind_ip_all"]
    ports:
    - containerPort: 27017
    volumeMounts:
    - name: mongo-storage
      mountPath: /data/db
  volumes:
  - name: mongo-storage
    persistentVolumeClaim:
      claimName: csi-pvc
```

1. Apply and verify:

```Shell
kubectl get pv
kubectl get pvc
kubectl get pods
```

1. Test data persistence:

```Shell
kubectl exec -it mongo-pod -- mongo
use mydb
db.mycollection.insert({ name: "Test", value: "This is a test" })
exit

kubectl delete pod mongo-pod
kubectl apply -f mongo.yml

kubectl exec -it mongo-pod -- mongo
use mydb
db.mycollection.find()
```

![Untitled 7 19.png](../../../../Images/Untitled%207%2019.png)

This process demonstrates automatic PV creation and data persistence in Kubernetes using Vultr's storage solution.

  

  

# Horizontal Pod Autoscaler

Horizontal Pod Autoscaler (HPA) in Kubernetes is an important feature for automatically scaling applications based on observed metrics. Here's an elaboration on the key points:

![Untitled 8 16.png](../../../../Images/Untitled%208%2016.png)

1. Definition and Purpose:
    - HPA automatically adjusts the number of pod replicas in deployments, replica sets, or stateful sets.
    - It scales based on observed metrics like CPU utilization or custom metrics.
    - The goal is to handle varying loads efficiently by scaling out (adding pods) when demand increases and scaling in (reducing pods) when demand decreases.
2. Horizontal Scaling:
    - This refers to adding more pods to the cluster, rather than increasing resources of existing pods.
    - It's called "horizontal" because it expands the application laterally (more instances) rather than vertically (more resources per instance).
3. Architecture:
    - HPA operates as a control loop in Kubernetes.
    - It runs intermittently, typically every 15 seconds, not continuously.
4. Components:
    - cAdvisor: A tool for collecting, aggregating, and exporting resource usage data from containers.
    - Metrics Server: A lightweight, in-memory metrics storage system that collects resource usage data (CPU, memory) from kubelets and exposes it via the Kubernetes API.
5. Installation and Usage:
    - The Metrics Server can be installed using kubectl:
        
        ```Shell
        kubectl apply -f <https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml>
        ```
        
    - Metrics can be viewed using commands like:
        
        ```Shell
        kubectl top pod -n kube-system
        kubectl top nodes -n kube-system
        ```
        
6. HPA Controller Operation:
    - The HPA controller sends requests to the API server to fetch metrics.
    - A sample request might look like:
        
        ```Shell
        GET https://[cluster-url]/apis/metrics.k8s.io/v1beta1/namespaces/default/pods
        ```
        

> This setup allows Kubernetes to automatically adjust the number of running pods based on actual resource usage or custom metrics, ensuring efficient resource utilization and application performance under varying loads.