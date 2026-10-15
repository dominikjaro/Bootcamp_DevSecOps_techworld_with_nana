## What is EKS Blueprints?

- Open-source project by AWS
- Makes it easier and faster to configure EKS clusters that are fully bootstrapped with the operational software that is needed to deploy and operate workloads.

### EKS Blueprints as solution

**EKS addresses this and helps manage:**

- the lifecycle of EKS clusters
- the operational software that runs in each cluster
- configuration for teams that need to run workloads in each cluster
- helps to implement relevant security controls and best practices

**Popular Kubernetes Add-ons**
- Amazon VPC CNI
- CoreDNS
- KubeProxy
- Cluster Autoscaler
- AWS Load Balancer Controller
- Argo CD
- Prometheus

---

### Cluster Autoscaler

- Component that automatically adjusts the size of a K8s cluster so that all pods have a place to run AND there are no unneeded Nodes.
- It's a K8s native component and enables this core feature of Kubernetes with huge benefit of reducing the need of manual operational work
- On AWS, Cluster Autoscaler uses Amazon EC2 Auto Scaling groups to dynamically adjust the number of nodes in the cluster based on the resource requirements of the pods.

1. When request for deployment comes in, K8s Scheduler determines whether Pods can be scheduled on the existing nodes.
2. If there are not enough resources on the current nodes, Pods will be set to **unschedulable**..
3. Once determined, Autoscaler will send a request to cloud provider for a new Node.

### Metrics Server

- Aggregator of resource usage data
- Collects resource metrics from Kubelets and exposes them in K8s API server through Metrics API
- Horizontal and Vertical Pod Autoscaling use these data to make scaling decisions

Use `kubectl top` to view the resource usage of nodes and pods in the cluster.

### AWS Load Balancer Controller

- Manages AWS Elastic Load Balancers for K8s cluster
- Use the controller to expose your cluster applications to the Internet

- The controller watches for changes to Ingress and Service resources and it creates the appropriate Load Balancing resources
- You can configure specific behavior by applying annotations to the Service or Ingress resources