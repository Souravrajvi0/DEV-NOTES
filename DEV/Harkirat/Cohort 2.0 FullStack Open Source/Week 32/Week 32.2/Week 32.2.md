---
view-count: 1
---
In this lecture, Harkirat covered the fundamentals of Docker Swarm, explaining its relationship with Docker and how it compares to Kubernetes. He discussed the architecture of Docker Swarm, including manager and worker nodes, and explored key concepts such as services, tasks, and containers. Harkirat demonstrated the practical aspects of Docker Swarm by guiding through the process of creating a two-node swarm and deploying a simple service, showcasing the ease of use and basic orchestration capabilities of Docker Swarm.

  

Recap Of Concepts

Docker Swarm

Core Concepts

Kubernetes vs Docker Swarm

Architecture

Services, Tasks & Containers

Services

Tasks

Containers

Relationship

Create a 2 Node Swarm

Deploying a Service

  

# Recap Of Concepts

Before diving into Docker Swarm specifically, let's clarify the relationships and differences between Docker, container orchestration engines, Docker Swarm, and Kubernetes:

1. Docker:  
    Docker is a platform for developing, shipping, and running applications in containers. It provides tools and a runtime to build and manage individual containers on a single host.  
    
2. Container Orchestration Engine:  
    A container orchestration engine is a system designed to manage containerized applications across multiple hosts. It handles deployment, scaling, load balancing, and monitoring of containers at scale.  
    
3. Docker Swarm:  
    Docker Swarm is Docker's native container orchestration solution. It's built into the Docker Engine and allows you to create and manage a cluster of Docker nodes as a single virtual system.  
    
4. Kubernetes:  
    Kubernetes is an open-source container orchestration platform originally developed by Google. It's more feature-rich and complex than Docker Swarm, and has become the industry standard for container orchestration.  
    

Relationship and differences:

- Docker provides the foundational technology for running containers, while container orchestration engines like Docker Swarm and Kubernetes build upon this to manage containers across multiple hosts.
- Docker Swarm is tightly integrated with Docker and uses the same CLI, making it easier to learn for those already familiar with Docker.
- Kubernetes is more powerful and flexible than Docker Swarm, but also more complex to set up and manage.
- Both Docker Swarm and Kubernetes serve the same primary purpose: orchestrating containerized applications across a cluster of machines.

Now, let's proceed with the Docker Swarm lecture:

# Docker Swarm

Docker Swarm is a container orchestration system built into the Docker Engine. It allows you to manage a cluster of Docker nodes as a single virtual system, simplifying the deployment and scaling of containerized applications.

Key points about Docker Swarm:

1. It's similar to Kubernetes in purpose, but generally considered easier to understand and set up.
2. Docker Swarm is not as widely used as Kubernetes in production environments, as Kubernetes has gained more industry adoption.
3. The core concepts in Docker Swarm include Services, Tasks, and Containers.

### Core Concepts

1. **Services**: In Docker Swarm, a service is the definition of the tasks to execute on the manager or worker nodes. It is the central structure of the swarm system and the primary root of user interaction with the swarm.
2. **Tasks**: A task is the atomic unit of scheduling within a swarm. When you declare a desired service state, the orchestrator realizes the desired state by scheduling tasks.
3. **Containers**: The container is an instance of a Docker image. Each task is associated with one container.

### Kubernetes vs Docker Swarm

While both serve similar purposes, there are some key differences:

1. **Complexity**:
    - Kubernetes: Very complex and can be challenging to understand.
    - Docker Swarm: Much easier to understand and implement.
2. **Production Readiness**:
    - Kubernetes: Widely adopted and considered more production-ready.
    - Docker Swarm: Not used as often in production environments.
3. **Scaling**:
    - Kubernetes: Supports autoscaling.
    - Docker Swarm: Requires manual scaling.
4. **CLI Tools**:
    - Kubernetes: Requires learning and using kubectl.
    - Docker Swarm: Works with the standard Docker CLI.

Despite being less popular than Kubernetes, Docker Swarm still offers a simpler alternative for container orchestration, especially for smaller-scale deployments or for teams already familiar with Docker.

  

  

# Architecture

The Docker Swarm architecture consists of two main types of nodes: Manager nodes and Worker nodes. Let's break down the architecture based on the provided image and information:

![Untitled 61.png](../../../../Images/Untitled%2061.png)

1. Manager Nodes:
    - The image shows three Manager nodes at the top, connected in a Raft consensus group.
    - Manager nodes are responsible for handling cluster management tasks.
    - They maintain the cluster state and schedule services.
    - Managers use an Internal distributed state store to maintain consistency across the cluster.
    - The Raft consensus algorithm is used to ensure agreement on the cluster state among managers.
2. Worker Nodes:
    - The image displays seven Worker nodes at the bottom.
    - Worker nodes are instances of Docker Engine dedicated to executing containers.
    - They receive and execute tasks assigned by the Manager nodes.
    - Workers form a Gossip network, which allows for efficient communication and information sharing across the cluster.
3. Communication:
    - Managers communicate with each other to maintain cluster state and make decisions.
    - Managers send tasks to Workers for execution.
    - Workers report their status back to Managers.
4. Scalability:
    - The architecture allows for easy scaling by adding more Worker nodes to handle increased workload.
    - Multiple Manager nodes provide fault tolerance and high availability for cluster management.
5. Load Distribution:
    - Manager nodes distribute tasks across Worker nodes, ensuring efficient resource utilization.

> This architecture provides a robust and scalable system for container orchestration, with clear separation of management and execution responsibilities between Manager and Worker nodes. The use of consensus algorithms and gossip protocols ensures consistency and efficient communication within the swarm.

  

  

  

# Services, Tasks & Containers

![Untitled 1 51.png](../../../../Images/Untitled%201%2051.png)

### **Services**

A service in Docker Swarm is the definition of how you want to run your application across the swarm. It specifies:

- The desired state of the application
- Number of replicas
- Docker image to use
- Command to run
- Other configurations like networks and volumes

In the image, we see a service defined as "3 nginx replicas" in the swarm manager. This service specification tells the swarm to maintain three instances of the nginx web server.

### **Tasks**

A task is a single instance of a service running on a node:

- Each task represents one container and its associated metadata
- For a service with multiple replicas, Docker Swarm creates a task for each replica

In the image, we can see three tasks (nginx.1, nginx.2, nginx.3) distributed across available nodes. Each task corresponds to one of the requested nginx replicas.

### **Containers**

A container is a running instance of a Docker image:

- Each task maps to one container
- The swarm orchestrator ensures tasks (and thus containers) are distributed across nodes according to service specifications

The image shows each task has an associated container (labeled as "nginx:latest"). These containers are the actual running instances of the nginx web server.

### **Relationship**

1. The service definition (3 nginx replicas) is created on the swarm manager.
2. The swarm manager creates three tasks to fulfill the service requirements.
3. Each task is scheduled on an available node.
4. On each node, the Docker engine creates a container for the assigned task.

This hierarchical structure (Service > Tasks > Containers) allows Docker Swarm to manage complex applications across multiple nodes while maintaining the desired state and distribution of the application components.

  

  

# Create a 2 Node Swarm

This section provides a hands-on guide to setting up a basic Docker Swarm cluster using two EC2 machines. Here's a breakdown of the steps:

1. Infrastructure Setup:
    - Create two EC2 machines on AWS.
    - Install Docker on both machines.
2. Initialize the Swarm:
    - On the first machine (which will become the manager node), run:
        
        ```Shell
        docker swarm init
        ```
        
    - This command initializes a new swarm and makes the current node a manager.
    - It will output a token and command for other nodes to join the swarm.
3. Join the Worker Node:
    - On the second machine (which will become a worker node), run the join command:
        
        ```Shell
        docker swarm join --token <TOKEN> <MANAGER-IP>:2377
        ```
        
    - Replace <TOKEN> and <MANAGER-IP> with the values provided by the `swarm init` command on the manager node.
4. Network Configuration:
    - Ensure that port 2377 is open on the manager node. This port is used for swarm management communication.
5. Verify the Swarm:
    - On the manager node, run:
        
        ```Shell
        docker node ls
        ```
        
    - This command lists all nodes in the swarm, confirming that both nodes have joined successfully.

Key points:

- The first node becomes the swarm manager, responsible for managing the cluster.
- The second node joins as a worker, ready to run tasks assigned by the manager.
- Port 2377 needs to be open for swarm communication.
- The `docker node ls` command provides an overview of the swarm's current state.

This setup creates a minimal Docker Swarm cluster, demonstrating the basic principles of swarm initialization and node joining. It's a foundation for more complex swarm deployments and services.

  

# Deploying a Service

This section provides a hands-on guide for deploying and managing a service in Docker Swarm. Let's break down the steps and explain each command:

1. Deploy the nginx service:
    
    ```Shell
    docker service create --replicas 3 --name helloworld -p 3000:80 nginx
    ```
    
    This command:
    
    - Creates a new service named "helloworld"
    - Deploys 3 replicas of the nginx image
    - Maps port 3000 on the host to port 80 in the container
2. Check the status of the service:
    
    ```Shell
    docker service ls
    ```
    
    This command lists all services in the swarm, showing their status, number of replicas, and other details.
    
3. Verify the service:  
    Access the service by navigating to  
    `your_machine_ip:3000` in a web browser. You should see the default nginx welcome page.
4. Test service resilience:  
    The instructions suggest deleting a few pods (containers) to observe if they automatically come back up. This demonstrates Docker Swarm's self-healing capabilities. You can use  
    `docker ps` to list containers and `docker rm -f <container_id>` to remove them.
5. Delete the service:
    
    ```Shell
    docker service rm helloworld
    ```
    
    This command removes the "helloworld" service from the swarm.
    

Key points:

- Docker Swarm automatically distributes the service replicas across available nodes.
- The service remains accessible even if individual containers fail, as Swarm maintains the desired number of replicas.
- Port mapping allows the service to be accessed from outside the swarm.
- Swarm ensures high availability by automatically replacing failed containers.

This hands-on exercise demonstrates the ease of deploying, scaling, and managing services in a Docker Swarm environment, showcasing its built-in orchestration capabilities.