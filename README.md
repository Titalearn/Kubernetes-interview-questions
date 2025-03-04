# Kubernetes-interview-questions
You will learn the top 20 kubernetes questions.
# Here are some possible answers to the Kubernetes questions you listed:
A *Was your Kubernetes experience ON-prem or managed Kubernetes?*
 My experiences with Kubernetes include both on-premises deployments and managed solutions like Amazon EKS (Elastic Kubernetes Service) and Google Kubernetes Engine.Managed environments often simplify cluster management and offer automatic updates, while on-premises deployments allow full control over the infrastructure.

B * What services are available on Kubernetes?*
In Kubernetes, you can find several services, including: - *ClusterIP Services*: internal access to the cluster. - *NodePort Services*: external access through a port associated with each node. - *LoadBalancer Services*: integration with a load balancer for external access. - *Ingress*: management of HTTP(S) request routing. - *Persistent Volumes*: persistent storage for applications.

 C *  What version of Kubernetes was this? *

 The latest stable release of Kubernetes is v1.32.2, which was released on February 11, 2025
 The specific version of Kubernetes can vary by project, but I have worked with several recent
versions, including 1.18 to 1.23.

D *  How many pods have you successfully deployed to this cluster? *
The number of pods deployed can vary greatly depending on the needs of the application,
but I have managed clusters that can contain several hundred to a few thousand pods,
depending on the capacity of the underlying infrastructure.

E *  In this mission, did you configure certificates? *

Yes, I configured SSL/TLS certificates to secure communications between services
in the cluster, often using tools like cert-manager.

F *  SSL and TLS: What's the difference?
SSL (Secure Sockets Layer) and TLS (Transport Layer Security) are security protocols
used to establish secure connections over the network. TLS is actually the successor to SSL,
providing improved security and more robust features. In practice, the term SSL
is often used interchangeably with TLS, although TLS is the current version.

G *How do you differentiate between development and production images?

Development images can include specific tags, for example myapp:dev
vs. myapp:prod. Additionally, we can have different configurations for the
environments, like environment variables or configuration files.

H * Has it ever happened that a pod shuts down or stops? *

Yes, this can happen for various reasons, such as errors in the application,
resource issues (cpu/memory), or planned outages on the nodes. Kubernetes typically handles this by automatically restarting pods based on
their configuration.

I * how  do you expose your  application to a service ?

To expose your application to a service, you typically follow these steps, especially in a Kubernetes environment:

1. Create a Deployment:
   - First, ensure your application is running in a Kubernetes cluster. You can create a Deployment to manage your application's pods.
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: my-app
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: my-app
     template:
       metadata:
         labels:
           app: my-app
       spec:
         containers:
         - name: my-app
           image: my-app-image:latest
           ports:
           - containerPort: 80
   ```

2. Create a Service:
   - Next, create a Service to expose your application. There are different types of Services you can use depending on your needs:
     - **ClusterIP**: Exposes the service on a cluster-internal IP. This is the default type.
     - **NodePort**: Exposes the service on each Node's IP at a static port.
     - **LoadBalancer**: Exposes the service externally using a cloud provider's load balancer.
     - **ExternalName**: Maps the service to a DNS name.

   Here’s an example of a Service of type `LoadBalancer`:
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: my-app-service
   spec:
     selector:
       app: my-app
     ports:
       - protocol: TCP
         port: 80
         targetPort: 80
     type: LoadBalancer
   ```

3. Apply the Configuration:
   - Apply the Deployment and Service configurations using `kubectl`:
   ```sh
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

4. Access the Application:
   - For a `LoadBalancer` service, Kubernetes will provision an external IP address that you can use to access your application. You can check the status and get the external IP using:
   ```sh
   kubectl get services
   ```

These steps will expose your application to the outside world, allowing users to access it via the external IP address or DNS name provided by the load balancer⁴⁵.


