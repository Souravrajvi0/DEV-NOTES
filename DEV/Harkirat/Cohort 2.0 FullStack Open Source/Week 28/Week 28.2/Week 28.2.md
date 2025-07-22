In this lecture, Harkirat covers two crucial Kubernetes resources: Secrets and ConfigMaps. He provides an in-depth exploration of their purposes, use cases, and implementation details. The lecture highlights the key differences between Secrets and ConfigMaps, explaining when and how to use each for managing application configurations and sensitive data.

  

  

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

Secrets in Kubernetes

Key Points about Secrets:

Creating and Using Secrets

Base64 Encoding

Secrets as Environment Variables

Best Practices

Considerations

ConfigMaps vs Secrets

Creating a ConfigMap

Creating a Secret

  

  

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

  

# Secrets in Kubernetes

Secrets are Kubernetes objects used to store sensitive information such as passwords, tokens, or keys. They provide a way to separate confidential data from application code and configuration.

![Untitled 55.png](../../../../Images/Untitled%2055.png)

### Key Points about Secrets:

1. **Purpose**: Store sensitive data securely within Kubernetes.
2. **API**: Part of the Kubernetes v1 API.
3. **Usage**: Can be mounted as environment variables or files in pods.
4. **Encoding**: Values are typically base64 encoded.

### Creating and Using Secrets

1. **Create a Secret and Pod**:

```YAML
apiVersion: v1
kind: Secret
metadata:
  name: dotfile-secret
data:
  .env: REFUQUJBU0VfVVJMPSJwb3N0Z3JlczovL3VzZXJuYW1lOnNlY3JldEBsb2NhbGhvc3QvcG9zdGdyZXMi
---
apiVersion: v1
kind: Pod
metadata:
  name: secret-dotfiles-pod
spec:
  containers:
    - name: dotfile-test-container
      image: nginx
      volumeMounts:
        - name: env-file
          readOnly: true
          mountPath: "/etc/secret-volume"
  volumes:
    - name: env-file
      secret:
        secretName: dotfile-secret
```

1. **Accessing the Secret in the Container**:
    
    ```Shell
    kubectl exec -it secret-dotfiles-pod /bin/bash
    cd /etc/secret-volume/
    ls
    ```
    

### Base64 Encoding

- Secrets use base64 encoding for values.
- This is not for security, but for standardization (e.g., handling binary data).
- Example: TLS certificates can contain non-ASCII characters.

### Secrets as Environment Variables

1. **Create a Secret**:

```YAML
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
data:
  username: YWRtaW4=  # base64 encoded 'admin'
  password: cGFzc3dvcmQ=  # base64 encoded 'password'
```

1. **Use Secret in a Pod**:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: secret-env-pod
spec:
  containers:
  - name: my-container
    image: busybox
    command: ["/bin/sh", "-c", "echo Username: $USERNAME; echo Password: $PASSWORD; sleep 3600"]
    env:
    - name: USERNAME
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: username
    - name: PASSWORD
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: password
```

### Best Practices

1. **Separation of Concerns**: Keep sensitive data separate from application code.
2. **Access Control**: Use RBAC to limit access to Secrets.
3. **Encryption**: Enable encryption at rest for Secrets in etcd.
4. **Minimal Exposure**: Only expose Secrets to pods that need them.

### Considerations

- Secrets are not encrypted by default in etcd.
- Base64 encoding is not encryption and doesn't provide security by itself.
- Consider using external secret management systems for enhanced security.

Secrets provide a convenient way to manage sensitive data in Kubernetes, but they should be used with appropriate security measures in place.

  

  

# ConfigMaps vs Secrets

This section compares ConfigMaps and Secrets, two Kubernetes resources used for managing configuration data, highlighting their key differences and use cases.

### Creating a ConfigMap

```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: example-config
data:
  key1: value1
  key2: value2
```

### Creating a Secret

```YAML
apiVersion: v1
kind: Secret
metadata:
  name: example-secret
data:
  password: cGFzc3dvcmQ=
  apiKey: YXBpa2V5
```

  

|   |   |   |
|---|---|---|
|Aspect|ConfigMaps|Secrets|
|Purpose|Store non-sensitive configuration data|Store sensitive data (passwords, tokens, keys)|
|Data Format|Plain text|Base64 encoded|
|Typical Content|Config files, env variables, CLI arguments|Passwords, OAuth tokens, SSH keys|
|Encoding|No encoding|Base64 encoded (not for security, but for transmission)|
|Update Frequency|Less frequent changes|More frequent rotation due to security needs|
|Kubernetes Features|Basic configuration injection|Integration with external secret management, encryption at rest support|
|Security Level|Standard|Higher priority in Kubernetes|
|Use in Pods|Mounted as files or env variables|Mounted as files or env variables with additional security|
|External Management|Limited support|Better integration with external systems (e.g., HashiCorp Vault)|
|Version Control|Can be stored directly|Should not be stored directly (only references)|
|Access Control|Generally more accessible|More stringent RBAC policies typically applied|
|Data Visibility|Easily viewable|Obfuscated (but not encrypted) by default|
|Size Limit|1MB|1MB|
|Use Case Example|Application config, feature flags|Database passwords, API keys|
|Encryption|Not encrypted|Can be encrypted at rest (when configured)|

> While both ConfigMaps and Secrets are used to decouple configuration from application code, they serve different purposes in terms of the sensitivity of the data they store. Understanding these differences is crucial for properly managing configuration and sensitive data in Kubernetes environments, ensuring both flexibility and security in your applications.