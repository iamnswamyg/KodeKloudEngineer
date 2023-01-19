
### 1. What is Kubernetes?
Kubernetes is an open-source container orchestration tool or system that is used to automate tasks such as the management, monitoring, scaling, and deployment of containerized applications. It is used to easily manage several containers (since it can handle grouping of containers), which provides for logical units that can be discovered and managed. It works brilliantly with all the cloud providers. So, we can say that Kubernetes is not a containerization platform, but it is a multi-container management solution. 

### 2. How is Kubernetes related to Docker?
- Docker is an open-source platform used to handle software development. Its main benefit is that it packages the settings and dependencies that the software/application needs to run into a container, which allows for portability and several other advantages. Docker builds the containers from images & provides the lifecycle management of containers. 
- Kubernetes: Kubernetes is used for orchestrate the individual containers. Kubernetes allows for the manual linking and orchestration of several containers, running on multiple hosts that have been created using Docker. These containers communicate with each other via Kubernetes. Containers running on multiple hosts can be manually linked and orchestrated using Kubernetes.

### 3. What is the difference between deploying applications on hosts and containers?
- Deploying applications on hosts: So, this kind of architecture will have an operating system and then the operating system will have a kernel that will have various libraries installed on the operating system needed for the application. So, in this kind of framework you can have n number of applications and all the applications will share the libraries present in that operating system.
- Deploying applications on containers: This kind of architecture will have a kernel and that is the only thing that’s going to be the only thing common between all the applications. So, if there’s a particular application that needs Java then that particular application we’ll get access to Java and if there’s another application that needs Python then only that particular application will have access to Python. So, the applications have the necessary libraries and binaries isolated from the rest of the system, and cannot be encroached by any other application.

### 4. What is Container Orchestration?
- Orchestration refers to the integration of multiple services that allows them to automate processes or synchronize information in a timely fashion. Say, for example, you have six or seven microservices for an application to run. If you place them in separate containers, this would inevitably create obstacles for communication. Orchestration would help in such a situation by enabling all services in individual containers to work seamlessly to accomplish a single goal.

### 5. What is the need for Container Orchestration?
- As orchestration means the amalgamation of all instruments playing together in harmony in music. Similarly, consider a scenario where you have 5-6 microservices for an application. Now, these microservices are put in individual containers, but won’t be able to communicate without container orchestration. Container orchestration means all the services in individual containers working together to fulfill the needs of a single server. To make sure that these containers communicate with each other we need container orchestration.

### 6. What are challenges Without Container Orchestration?
There were also many challenges that came into place without the use of container orchestration. So, to overcome these challenges the container orchestration came into place.
- Incereases the human cost of running services.
- Increases the complexity of something new in production
- Setting up services manually
- Increasesthe size of bills from cloud providers
- Scalling will be difficult
- Manual work of fixing if a node crashes

### 7. What are the features of Kubernetes?
- Kubernetes places control for the user where the server will host the container. It will control how to launch. So, Kubernetes automates various manual processes. 
- Kubernetes manages various clusters at the same time. 
- Kubernetes self-monitors the health of nodes and containers. 
- Automated Scheduling: Kubernetes provides advanced scheduler to launch container on cluster nodes.
- Self Healing: Rescheduling, replacing and restarting the containiers which are dead.
- Automated rollout & rollbacks: Kubernetes supports rollouts and rollbacks for the desired state of the containerized application.
- Horizontal Scaling & Load Balancing: Kubernetes can scale up and scale down the application as per the requirements. With Kubernetes, users can scale resources not only vertically but also horizontally that too easily and quickly.
- It provides various additional services like management of containers, security, networking, and storage. 

### 8. How does Kubernetes simplify containerized Deployment?
As a typical application would have a cluster of containers running across multiple hosts, all these containers would need to talk to each other. So, to do this you need something big that would load balance, scale & monitor the containers. Since Kubernetes is cloud-agnostic and can run on any public/private providers it must the simplified choice for containerized deployment.

### 9. What do you know about clusters in Kubernetes?
The fundamental behind Kubernetes is that we can enforce the desired state management, by which I mean that we can feed the cluster services of a specific configuration, and it will be up to the cluster services to go out and run that configuration in the infrastructure. The deployment file will have all the configurations required to be fed into the cluster services. Now, the deployment file will be fed to the API and then it will be up to the cluster services to figure out how to schedule these pods in the environment and make sure that the right number of pods are running.

### 10. What is Google Container Engine or Google Kubernetes Engine?
Google Container Engine (GKE) is an open-source management platform for Docker containers and clusters. This Kubernetes based engine supports only those clusters which run within Google’s public cloud services. Google Container Engine is renamed as Google Kubernetes Engine.

### 11. What is Heapster?
Heapster is a cluster-wide aggregator of data provided by Kubelet running on each node. This container management tool is supported natively on Kubernetes cluster and runs as a pod, just like any other pod in the cluster. So, it basically discovers all nodes in the cluster and queries usage information from the Kubernetes nodes in the cluster, via on-machine Kubernetes agent.

### 12. What is Minikube?
Minikube is a tool that makes it easy to run Kubernetes locally. This runs a single-node Kubernetes cluster inside a virtual machine.

### Q13. What is Kubectl?
Kubectl is the platform using which you can pass commands to the cluster. So, it basically provides the CLI to run commands against the Kubernetes cluster with various ways to create and manage the Kubernetes component.

### 14. What is Kubelet?
The kubelet is a service agent that controls and maintains a set of pods by watching for pod specs through the Kubernetes API server. It preserves the pod lifecycle by ensuring that a given set of containers are all running as they should. The kubelet runs on each node and enables the communication between the master and slave nodes.

### 15. What do you understand by a node in Kubernetes?
- A node in kubernetes cluster is the main worker machine.
- They are also known as minions.
- It could run on a physcial machine or a VM.
- Node provides all the necessary services to run Pods.
- Node in the kubernetes system is managed by the master.

### 16. What are the different components of Kubernetes Architecture?
The Kubernetes Architecture has mainly 2 components – the master node and the worker node. The master and the worker nodes have many inbuilt components within them. 
- Master node: It has the kube-controller-manager, kube-apiserver, kube-scheduler, etcd.
- Worker node: It has kubelet and kube-proxy running on each node.

### 17. Explain components of Kubernetes Architecture?
1. Master Node:
The master node dignifies the node that controls and manages the set of worker nodes. This kind resembles a cluster in Kubernetes. The nodes are responsible for the cluster management and the API used to configure and manage the resources within the collection. The master nodes of Kubernetes can run with Kubernetes itself, the asset of dedicated pods.
- etcd: etcd is a distributed key-value store that is used by Kubernetes to store the cluster's configuration data.
- kube-scheduler: The scheduler is a component of Kubernetes that is responsible for assigning pods (groups of containers) to nodes in the cluster.
- kube-apiserver: This kind validates and provides configuration data for the API objects. It includes pods, services, replication controllers. Also, it provides REST operations and also the frontend of the cluster. This frontend cluster state is shared through which all other component interacts. The API server is the central control plane component of Kubernetes and is responsible for exposing the API that is used to interact with the cluster.
- kube-controller-manager: The controller manager is a daemon that runs various controllers that are responsible for maintaining the desired state of the cluster, such as replicasets and deployments.
2. Worker Node:
A node is the smallest fundamental unit of computing hardware. It represents a single machine in a cluster, which could be a physical machine in a data center or a virtual machine from a cloud provider. Each machine can substitute any other machine in a Kubernetes cluster.  
- Kubelet: The kubelet is a daemon that runs on each node in the cluster and is responsible for communicating with the control plane and ensuring that containers are running as intended on the node.
- kube-proxy: The kube-proxy is a daemon that runs on each node in the cluster and is responsible for implementing the network proxying and load balancing functionality of Kubernetes.
- Container runtime: The container runtime is the software that is responsible for running containers on the nodes in the cluster. Examples of container runtimes include Docker and containerd.
3. Client:
- kubectl: kubectl is the command-line interface (CLI) for interacting with a Kubernetes cluster.

### 18. What do you understand by Kube-proxy?
- Kube-proxy is an implementation of a load balancer and network proxy used to support service abstraction with other networking operations. Kube-proxy is responsible for directing traffic to the right container based on IP and the port number of incoming requests.
- Kube-proxy can run on each and every node and can do simple TCP/UDP packet forwarding across backend network service. So basically, it is a network proxy that reflects the services as configured in Kubernetes API on each node. So, the Docker-linkable compatible environment variables provide the cluster IPs and ports which are opened by proxy.

### 19. Can you brief on the working of the master node in Kubernetes?
Kubernetes master controls the nodes and inside the nodes the containers are present. Now, these individual containers are contained inside pods and inside each pod, you can have a various number of containers based upon the configuration and requirements. So, if the pods have to be deployed, then they can either be deployed using user interface or command-line interface. Then, these pods are scheduled on the nodes, and based on the resource requirements, the pods are allocated to these nodes. The kube-apiserver makes sure that there is communication established between the Kubernetes node and the master components.

### 20. What is the role of kube-apiserver and kube-scheduler?
- kube–apiserver: It follows the scale-out architecture and is the front end of the master node control panel. This exposes all the APIs of the Kubernetes Master node components and is responsible for establishing communication between Kubernetes Node and the Kubernetes master components.
- kube-scheduler: It is responsible for distributing and managing the workload on the worker nodes. So, it selects the most suitable node to run the unscheduled pod based on resource requirements and keeps track of resource utilization. It ensures that the workload is not scheduled on already full nodes.

### 21. What does the node status contain?
The main components of a node status are Address, Condition, Capacity, and Info.

### 22. What process runs on Kubernetes Master Node? 
The Kube-api server process runs on the master node and serves to scale the deployment of more instances.

### 23. What is a pod in Kubernetes?
Pods are high-level structures that wrap one or more containers. This is because containers are not run directly in Kubernetes. Containers in the same pod share a local network and the same resources, allowing them to easily communicate with other containers in the same pod as if they were on the same machine while at the same time maintaining a degree of isolation.

### 24. What is a cluster of containers in Kubernetes? 
A cluster of containers is a set of machine elements that are nodes. Clusters initiate specific routes so that the containers running on the nodes can communicate with each other. In Kubernetes, the container engine (not the server of the Kubernetes API) provides hosting for the API server.

### 25. What are Daemon sets?
A Daemon set is a set of pods that runs only once on a host. They are used for host layer attributes like a network or for monitoring a network, which you may not need to run on a host more than once.

### 26. What is ‘Heapster’ in Kubernetes?
 A Heapster is a performance monitoring and metrics collection system for data collected by the Kublet. This aggregator is natively supported and runs like any other pod within a Kubernetes cluster, which allows it to discover and query usage data from all nodes within the cluster. Heapster provides metric collection, basic monitoring capabilities and supports multiple data sinks to write the collected metrics to. The code for each sink resides within the Heapster repository. Heapster also enables the use of the Horizontal Pod Autoscaler to autoscale on metrics. Heapster datastore most of the time is InfluxDB.

### 27. What is Minikube?
With the help of Minikube, users can Kubernetes locally. This process lets the user run a single-node Kubernetes cluster on your personal computer, including Windows, macOS, and Linus PCs. With this, users can try out Kubernetes also for daily development work.

### 28. What is a Namespace in Kubernetes?
Namespaces are used for dividing cluster resources between multiple users. They are meant for environments where there are many users spread across projects or teams and provide a scope of resources.

### 29. Name the initial namespaces from which Kubernetes starts?
- Default
- Kube – system
- Kube – public

### 30. What is the Kubernetes controller manager?
- The controller manager is a daemon that runs in the background and manages the state of the system by reconciling the desired state specified by users with the current state of the system. This is done by continuously monitoring the state of the system and making adjustments as needed to bring the system into alignment with the desired state. The controller manager is responsible for a variety of tasks such as replicating pods, managing service endpoints, and performing rolling updates. 
- Multiple controller processes run on the master node but are compiled together to run as a single process, the Kubernetes Controller Manager. So, Controller Manager is a daemon that embeds controllers and does namespace creation and garbage collection. It owns the responsibility and communicates with the API server to manage the end-points.
- The controller manager is used for embedding core control loops(reconcilation), garbage collection, and Namespace creation. The Controller Manager does not directly modify resources in the Kubernetes cluster. Instead, it manages multiple controllers responsible for specific activities—including replication controllers, endpoint controllers, namespace controllers, node controllers, token controllers and service account controllers.

### 31. What is etcd?
- Kubernetes uses etcd as a distributed key-value store for all of its data, including metadata and configuration data, and allows nodes in Kubernetes clusters to read and write data. Although etcd was purposely built for CoreOS, it also works on a variety of operating systems (e.g., Linux, BSB, and OS X) because it is open-source. Etcd represents the state of a cluster at a specific moment in time and is a canonical hub for state management and cluster coordination of a Kubernetes cluster.
- etcd is written in Go programming language and is a distributed key-value store used for coordinating distributed work. So, Etcd stores the configuration data of the Kubernetes cluster, representing the state of the cluster at any given point in time.

### 32. What are the different services within Kubernetes?
Different types of Kubernetes services include: 
- Cluster IP service
- Node Port service
- External Name Creation service  
- Load Balancer service

### 33. What is ClusterIP?
The ClusterIP is the default Kubernetes service that provides a service inside a cluster (with no external access) that other apps inside your cluster can access. 

### 34. What is NodePort? 
The NodePort service is the most fundamental way to get external traffic directly to your service. It opens a specific port on all Nodes and forwards any traffic sent to this port to the service.

### 35. What is the LoadBalancer? 
- The LoadBalancer service is used to expose services to the internet. A Network load balancer, for example, creates a single IP address that forwards all traffic to your service. The LoadBalancer service routes traffic between multiple nodes.
- A static IP for the Kubernetes load balancer can be achieved by changing DNS records since the Kubernetes Master can assign a new static IP address.

### 36. What is the ExternalName Creation service? 
The ExternalName Service acts as a proxy, allowing a user to redirect requests to a service sitting outside (or inside) the cluster. Essentially it creates a CNAME record that connects the DNS name to some cluster-local name—that way your pods can leverage that service.

### 37. What is the Ingress network, and how does it work?
 - An ingress is an object that allows users to access your Kubernetes services from outside the Kubernetes cluster. Users can configure the access by creating rules that define which inbound connections reach which services.
- This is an API object that provides the routing rules to manage the external users' access to the services in the Kubernetes cluster through HTTPS/ HTTP. With this, users can easily set up the rules for routing traffic without creating a bunch of load balancers or exposing each service to the nodes.

### 38. What do you understand by Cloud controller manager?
- Cloud Controller Manager is the control panel component that embeds the cloud-specific control logic. This process lets you link the cluster into the cloud provider's API and separates the elements that interact with the cloud platform from components that only interact with your cluster. 
- This also enables the cloud providers to release the features at a different pace compared to the main Kubernetes project. It is structured using a plugin mechanism and allows various cloud providers to integrate their platforms with Kubernetes.

### 39. What is Container resource monitoring?
This refers to the activity that collects the metrics and tracks the health of containerized applications and microservices environments. It helps to improve health and performance and also makes sure that they operate smoothly.

### 40. What is the difference between a replica set and a replication controller?
1. Replication controller: It is a wrapper on a pod. This provides additional functionality to the pods, which offers replicas. It monitors the pods and automatically restarts them if they fail. If the node fails, this controller will respawn all the pods of that node on another node. If the pods die, they won't be spawned again unless wrapped around a replication controller. 
2. Replica Set: It is the next-generation replication controller. This kind of support has some selector types and supports the equality-based and the set-based selectors. It allows filtering by label values and keys. To match the object, they have to satisfy all the specified label constraints.
    - Equity-Based Selectors: This type of selector allows filtering by label key and values. So, in layman’s terms, the equity-based selector will only look for the pods with the exact same phrase as the label.
        - Example: Suppose your label key says app=nginx; then, with this selector, you can only look for those pods with label app equal to nginx.
    - Selector-Based Selectors: This type of selector allows filtering keys according to a set of values. So, in other words, the selector-based selector will look for pods whose label has been mentioned in the set.
        - Example: Say your label key says app in (Nginx, NPS, Apache). Then, with this selector, if your app is equal to any of Nginx, NPS, or Apache, the selector will take it as a true result.

### 41. What is a headless service?
- Headless service is a regular Kubernetes service which is used for creating a service grouping. That does not allocate an IP address or forward traffic. So you can do this by explicitly setting spec.clusterIP to “None” and spec.type is set to "ClusterIP" in the mainfest file, which means no cluster IP is allocated. They are used in creating Statefulsets. 
- For example, if you host MongoDB on a single pod. And you need a service definition on top of it for taking care of the pod restart and also for acquiring a new IP address but you don’t want any load balancing or routing. You just need the headless service to patch the request to the back-end pod. 
- This service enables you to directly reach the pods without the need to access them through a proxy.

### 42. What are federated clusters?
The aggregation of multiple clusters that treat them as a single logical cluster refers to cluster federation. In this, multiple clusters may be managed as a single cluster. They stay with the assistance of federated groups. Also, users can create various clusters within the data center or cloud and use the federation to control or manage them in one place. 
You can perform cluster federation by doing the following: 
- Cross cluster that provides the ability to have DNS and Load Balancer with backend from the participating clusters. 
- Users can sync resources across different clusters in order to deploy the same deployment set across the various clusters.

### 43. Give examples of recommended security measures for Kubernetes.
Examples of standard Kubernetes security measures include:
- defining resource quotas
- support for auditing
- restriction of etcd access
- regular security updates to the environment
- network segmentation
- definition of strict resource policies
- continuous scanning for security vulnerabilities
- using images from authorized repositories.

### 44. What is Ingress network, and how does it work?
- Ingress network is a collection of rules that acts as an entry point to the Kubernetes cluster. This allows inbound connections, which can be configured to give services externally through reachable URLs, load balance traffic, or by offering name-based virtual hosting. So, Ingress is an API object that manages external access to the services in a cluster, usually by HTTP and is the most powerful way of exposing service.

### 45. What do you understand by Cloud controller manager?
1. The Cloud Controller Manager is responsible for persistent storage, network routing, abstracting the cloud-specific code from the core Kubernetes specific code, and managing the communication with the underlying cloud services. It might be split out into several different containers depending on which cloud platform you are running on and then it enables the cloud vendors and Kubernetes code to be developed without any inter-dependency. So, the cloud vendor develops their code and connects with the Kubernetes cloud-controller-manager while running the Kubernetes.
2. The various types of cloud controller manager are as follows:
    - Node Controller: It checks and confirms that node is deleted properly after it has been stopped.
    - Route Controller: The route controller manages the traffic routes in the underlying cloud infrastructure.
    - Volume Controller: Manages the storage volume and interacts with the cloud provider to orchestrate volume.
    - Service Controller: The service controller responsible for the management of cloud provide load balancers.

### 46. What is Container resource monitoring?
As for users, it is really important to understand the performance of the application and resource utilization at all the different abstraction layer, Kubernetes factored the management of the cluster by creating abstraction at different levels like container, pods, services and whole cluster. Now, each level can be monitored and this is nothing but Container resource monitoring.
1. To use Prometheus and cAdvisor together in a Kubernetes cluster, you would first deploy Prometheus as a Kubernetes deployment or daemonset. Then, you would deploy cAdvisor as a daemonset on each node in the cluster. Finally, you would configure Prometheus to scrape the cAdvisor metrics endpoint, which is typically exposed on each node's IP at a specific port.
    - Prometheus is a monitoring system that scrapes metrics from targets, stores them in a time-series database, and allows you to query and alert on those metrics. Prometheus can also be configured it to scrape the Heapster metrics endpoint which is typically exposed on the Kubernetes API server.
    - cAdvisor (short for "container advisor") is a tool that runs on each node in a Kubernetes cluster and collects performance metrics for all the containers running on that node. It can be configured to export these metrics to Prometheus, which can then scrape and store them.
2. Heapster is in the process of being deprecated and replaced by Prometheus Operator. Heapster, InfluxDB, and Grafana can be used together as an alternative to Prometheus and cAdvisor for monitoring a Kubernetes cluster. Deploy Heapster, InfluxDB,Grafana as a pods. Heapster will collect resource usage and performance metrics from the Kubernetes API server and store them in memory. Heapster will forward the metrics it collects to InfluxDB for storage. Configure Grafana to connect to the InfluxDB instance and create a dashboard to visualize the metrics. Grafana will use the metrics stored in InfluxDB to create interactive and informative dashboards. 
   - Heapster is a Kubernetes-native resource usage and performance analysis agent. It can be used to collect and store cluster-wide metrics and events. It can also be configured to export metrics to InfluxDB.
   - InfluxDB is a time-series database that can be used to store metrics collected by Heapster.
   - Grafana is a dashboard and visualization tool that can be used to create interactive and informative dashboards from metrics stored in InfluxDB.

### 47. Suppose a company built on monolithic architecture handles numerous products. Now, as the company expands in today’s scaling industry, their monolithic architecture started causing problems. How do you think the company shifted from monolithic to microservices and deploy their services containers?
- As the company’s goal is to shift from their monolithic application to microservices, they can end up building piece by piece, in parallel and just switch configurations in the background. Then they can put each of these built-in microservices on the Kubernetes platform. So, they can start by migrating their services once or twice and monitor them to make sure everything is running stable. Once they feel everything is going good, then they can migrate the rest of the application into their Kubernetes cluster.

### 48. Consider a multinational company with a very much distributed system, with a large number of data centers, virtual machines, and many employees working on various tasks. How do you think can such a company manage all the tasks in a consistent way with Kubernetes?
- As all of us know that IT departments launch thousands of containers, with tasks running across a numerous number of nodes across the world in a distributed system.
-  In such a situation the company can use something that offers them agility, scale-out capability, and DevOps practice to the cloud-based applications.
- So, the company can, therefore, use Kubernetes to customize their scheduling architecture and support multiple container formats. This makes it possible for the affinity between container tasks that gives greater efficiency with an extensive support for various container networking solutions and container storage.

### 49. Consider a situation, where a company wants to increase its efficiency and the speed of its technical operations by maintaining minimal costs.How do you think the company will try to achieve this?
- The company can implement the DevOps methodology, by building a CI/CD pipeline, but one problem that may occur here is the configurations may take time to go up and running. So, after implementing the CI/CD pipeline the company’s next step should be to work in the cloud environment. Once they start working on the cloud environment, they can schedule containers on a cluster and can orchestrate with the help of Kubernetes. This kind of approach will help the company reduce their deployment time, and also get faster across various environments.

### 50. Suppose a company wants to revise it’s deployment methods and wants to build a platform which is much more scalable and responsive. How do you think this company can achieve this to satisfy their customers?
- In order to give millions of clients the digital experience they would expect, the company needs a platform that is scalable, and responsive, so that they could quickly get data to the client website. Now, to do this the company should move from their private data centers (if they are using any) to any cloud environment such as AWS. Not only this, but they should also implement the microservice architecture so that they can start using Docker containers. Once they have the base framework ready, then they can start using the best orchestration platform available i.e. Kubernetes. This would enable the teams to be autonomous in building applications and delivering them very quickly.

### 51. Consider a multinational company with a very much distributed system, looking forward to solving the monolithic code base problem. How do you think the company can solve their problem?
- Well, to solve the problem, they can shift their monolithic code base to a microservice design and then each and every microservices can be considered as a container. So, all these containers can be deployed and orchestrated with the help of Kubernetes.

### 52. All of us know that the shift from monolithic to microservices solves the problem from the development side, but increases the problem at the deployment side. How can the company solve the problem on the deployment side?
- The team can experiment with container orchestration platforms, such as Kubernetes and run it in data centers. So, with this, the company can generate a templated application, deploy it within five minutes, and have actual instances containerized in the staging environment at that point. This kind of Kubernetes project will have dozens of microservices running in parallel to improve the production rate as even if a node goes down, then it can be rescheduled immediately without performance impact.

### 53. Suppose a company wants to optimize the distribution of its workloads, by adopting new technologies. How can the company achieve this distribution of resources efficiently?
- The solution to this problem is none other than Kubernetes. Kubernetes makes sure that the resources are optimized efficiently, and only those resources are used which are needed by that particular application. So, with the usage of the best container orchestration tool, the company can achieve the distribution of resources efficiently.

### 54. Consider a carpooling company wants to increase their number of servers by simultaneously scaling their platform. How do you think will the company deal with the servers and their installation?
The company can adopt the concept of containerization. Once they deploy all their application into containers, they can use Kubernetes for orchestration and use container monitoring tools like Prometheus to monitor the actions in containers. So, with such usage of containers, giving them better capacity planning in the data center because they will now have fewer constraints due to this abstraction between the services and the hardware they run on.

### 55. Consider a scenario where a company wants to provide all the required hand-outs to its customers having various environments.How do you think they can achieve this critical target in a dynamic manner?
- The company can use Docker environments, to put together a cross-sectional team to build a web application using Kubernetes. This kind of framework will help the company achieve the goal of getting the required things into production within the shortest time frame. So, with such a machine running, the company can give the hands-outs to all the customers having various environments.

### 56. Suppose a company wants to run various workloads on different cloud infrastructure from bare metal to a public cloud. How will the company achieve this in the presence of different interfaces?
- The company can decompose its infrastructure into microservices and then adopt Kubernetes. This will let the company run various workloads on different cloud infrastructures.

### 57. Can a Pod have multiple IP address assigned. Whether that Pod contains one or more containers.
- A Pod in Kubernetes can have multiple IP addresses assigned to it, but it is less common in a single container pod.
- By default, a Pod in Kubernetes is assigned a single IP address, which is shared by all the containers in the Pod. This IP address is used for communication within the cluster.
- In case of multiple containers in a pod, each container can be assigned with its own IP address, this is called container-to-container communication, and it enables the containers to communicate with each other directly.
- However, if you want to assign multiple IP addresses to a single container pod, you can use a feature called IP Aliases. IP Aliases allows you to assign multiple IP addresses to a single network interface on a pod, but it requires a specific network plugin that supports it, also this is not a common use case.

### 58. How can we find who is the owner of a POD or a Deployment, so that we can reach to their Team?
- You can find the owner of a POD or Deployment in a Kubernetes cluster by looking at the metadata section of the resource’s configuration. The metadata section contains information about the resource, including information about the resource’s owner.
- For a POD, you can use the kubectl describe pod command followed by the name of the POD you want to inspect. The output will include a section called Labels which will contain the information of the owner.
- For a Deployment, you can use the kubectl describe deployment command followed by the name of the Deployment you want to inspect. The output will include a section called Labels which will contain the information of the owner.
- If the owner information is not present in the Labels, you can look for Annotations section , it may contain the information of the owner.
- Once you have the information of the owner, you can reach out to their team using the contact information provided in the owner information.

### 59. If we add a Master node in cluster, how will the previous kublets know the location of this new Master node?
- When a new Master node is added to a cluster, the existing Kubernetes nodes (also known as kublets) will not automatically know the location of the new Master. However, the administrator can update the cluster’s configuration to point the kublets to the new Master node, which will allow them to communicate with it and join the cluster. This can typically be done by updating the cluster’s kubeconfig file or by modifying the kublet’s configuration on each individual node.

### 60. What is Helm?
Helm Charts assist you in defining, installing, and upgrading even the most complicated Kubernetes application. ... Helm is a CNCF-graduated project that is supported by the Helm community.

### 61. What are the advantages of Helm?
Helm helps in three ways: 
- increases productivity
- reduces the complexity of microservice deployments
- allows for the adoption of cloud native applications.

### 62. How does Helm work?
Helm is used in deploying charts as a package application, they are a collection of our pre configured application resources that can be deployed as a unit. We can deploy another version of its charts with different sets of configuration.

### 63. What are the concepts used in Helm?
Concepts used by Helm are:
- Chart: It is a package consists of pre configured Kubernetes Resources.
- Release: It is an instance that can be deployed to the Cluster with the help of Helm.
- Repository: It is a group of charts that are available for others.

### 64. Why to use Helm?
- It can be time consuming and tedious to write and maintain Kubernetes YAML manifests for all of the essential Kubernetes objects. You'll need at least three YAML manifests with duplicated and hardcoded values for the most basic deployments. Helm streamlines the process by generating a single package that can be distributed across your cluster.
- Helm is a client/server application that relied on Tiller (the helm server) to be installed in your cluster. Helm is similar to RPM and DEB packages in Linux, and it allows developers to package and ship applications to their end customers for installation.
- Once you've installed and configured Helm (details below), you may use one simple helm install command to install production-ready apps from software providers like MongoDB, MySQL, and others into your Kubernetes cluster.

### 65. What are Helm charts?
Helm offers packaging format called charts. Helm Charts are a collection of Kubernetes YAML manifests that can be published to your Kubernetes clusters as a single package. Installing a Helm Chart into your cluster after it has been packaged is as simple as running a single helm install, greatly simplifying the deployment of containerized apps.

### 66. How to create Helm charts?
When we create a new chart in Helm, it has a specific structure. We can use run helm create YOUR-CHART-NAME command to create helm chart. 
- .helmignore: This folder contains all of the files that should be ignored when packing the chart. If you're familiar with git, this is similar to.gitignore.
- Chart.yaml: User can write all of the details regarding the chart you're packaging. So, for instance, your version number, and so on. This is where you'll record all of your information.
- Values.yaml: User can define all of the values that will get use in templates. Consider helms variable.tf file, if you're familiar with Terraform.
Charts: This is where user can keep other charts on which user's chart is based. User might be referring to another chart that is required for user's chart to perform properly.
Templates: This folder contains the actual manifest that will be used with the chart.

### 67. Explain the architecture of Helm?
Helm is a two-part executable: the Helm Client and the Helm Library.
- The Helm Client is a command-line client for end users. Local chart development, Managing repositories, Managing releases, Interfacing with the Helm library, Sending charts to be installed, Requesting upgrades or uninstalls of existing releases are all responsibilities of the client.
- The Helm Library contains the logic that allows all Helm operations to be performed effectively. It interacts with the Kubernetes API server to provide the capabilities such as combining a chart and configuration to generate a release, installing charts into Kubernetes and delivering the subsequent release object, upgrading and uninstalling charts by dealing with Kubernetes. The Helm logic is encapsulated in the independent Helm library, allowing it to be used by a variety of clients.
-   - The Helm client and library is written in the Go programming language. To communicate with Kubernetes, the library use the Kubernetes client library. That library currently uses REST+JSON. It keeps information in Secrets which reside in Kubernetes. It is not required to have its own database. When feasible, configuration files are written in YAML.

### 68. Why is Tiller required in Helm 2?
- Tiller was a server-side component that was used to keep track of the current state of the Helm release. It also keeps track of all release information in a config-map for each release in the same namespace as tiller. This config-map is utilised by helm whenever we try to upgrade a specific version, and it compares the new manifest to the existing configs.

### 69. Why is Tiller removed from Helm 3?
- Helm uses Tiller to deploy the Kubernetes object. Because Kubernetes did not support RBAC policies when Helm 2 was launched, Helm took the maximum permission to make changes in Kubernetes by default. If Helm has not been correctly installed, this can lead to security vulnerabilities in the cluster. However, since RBAC is enabled by default in Kubernetes 1.6, there is no need for Helm to keep track of who is allowed to install what, as the same function can now be done natively by Kubernetes, which is why tiller was removed entirely in Helm 3.

### 70. What has been changed regarding namespace in Helm 3?
The scope of the release name is now restricted to the namespace in which it is deployed. The release name used to be required to be unique across the cluster, but it is now restricted to a particular namespace.

- Earlier in Helm2, we would do something like this to deploy a service, such as mysql:
```
Deployment 1: helm install stable/mysql --name mysql-develop --namespace develop
Deployment 2: helm install stable/mysql --name mysql-qa --namespace qa
```
- In Helm3, the same deployment can now be accomplished as follows:
```
Deployment 1: helm install stable/mysql --name mysql --namespace develop
Deployment 2: helm install stable/mysql --name mysql --namespace qa
```

### 71. What are the benefits of using secrets in Helm 3?
Config-maps were used in Helm 2 to hold release information. In Helm 3, secrets are used instead as the default storage driver.
Helm 2 does not keep the release information directly, instead, it encrypts it before storing it in config-map. Furthermore, while retrieving such configs, helm must repeat those processes in order to decrypt the data. Having secrets in place makes the entire process easier. Helm 3 collects the secrets, decrypts them, and then applies them.

### 72. How does helm chart dependencies work?
In Helm, a chart can have dependencies on other charts. These dependencies are specified in the Chart.yaml file of the chart using the dependencies field. When a chart is installed, Helm will automatically download and install any charts listed as dependencies before installing the chart itself. This allows charts to easily depend on other charts and reuse common components. When updating or deleting a chart, Helm will also take care of updating or deleting its dependencies as well. Dependencies can also be defined in requirements.yaml file.
```
apiVersion: v2
name: mychart
dependencies:
  - name: nginx-ingress
    version: 1.40.2
    repository: https://kubernetes-charts.storage.googleapis.com
  - name: prometheus
    version: 9.2.1
    repository: https://kubernetes-charts.storage.googleapis.com
```
When you run helm install on mychart, Helm will automatically download and install the nginx-ingress and prometheus charts before installing mychart.

### 73. Which of the different types of fields needed to be specified for dependencies in Helm Chart?
Different types of fields needed are as follows:
- name
- version
- repository

### 74. How can we install a specific Chart version in Helm?
We can use Prometheus in installing a specific chart version:
helm install -f source/prometheus/values.yaml prometheus –name source –namespace –version 6.7.4

### 75. How can we set multiple values with Helm?
We can set multiple values by using the following helm command:
helm install–set favoriteFood=junk./mychart

### 76. How does Helm updates Kubernetes?
Helm updates Kubernetes clusters by using the command given:
helm upgrades -d ingress-controller/values.yml nginx-ingress stable/nginx-ingress

### 77. How do we list all the available charts under a Helm Repo?
We can list all the charts by using the following command:
helm search repo [namespace]

### 78. How do we validate Helm Chart content?
We can validate Helm Chart contents by using the following command:
helm install –abcd –debug ./mychart

### 79. How can we uninstall Helm Chart on specific resource?
We can uninstall Helm Chart by using the following command, we should not use slash(/) in the command:
helm delete redis –example

### 80. Does helm still use Tiller?
With Tiller now gone, the security model for Helm is radically simplified. By removing Tiller, Helm 3 supports all the modern security, identity, and authorization features of modern Kubernetes.

### 81. What is replicaCount in helm?
Command-line parameter. Cluster management console field. compute.replicaCount. Replica count. Number of pod replicas for the compute container.

### 82. What is _helpers TPL in helm?
tpl? Helm allows for the use of Go templating in resource files for Kubernetes. A file named _helpers.tpl is usually used to define Go template helpers with this syntax:
```
 {{- define “yourFnName” -}} {{- printf “%s-%s” .Values.name .Values.version | trunc 63 -}} {{- end -}}
 ```

### 83. Can a helm chart have multiple deployments?
Let’s assume you’re deploying a database with Kubernetes—including multiple deployments, containers, secrets, volumes, and services. Helm allows you to install the same database with a single command and a single set of values.

### 84. Where do you store helm charts?
All template files are stored in a chart’s templates/ folder. When Helm renders the charts, it will pass every file in that directory through the template engine.

### 85. Where are helm repos stored locally?
The official Helm repo URL is https://kubernetes-charts.storage.googleapis.com . This repo is mainteined on GitHub and it’s URL is https://github.com/helm/charts. So the best approach is to clone the official repo github and work on it locally.

### 86. What is Helm values yaml?
yaml. All Helm packed applications have an associated values. yaml file which dictates the configuration of an application. By design many applications ship with a default values.

### 87. What is Umbrella chart in helm?
Helm charts have the ability to include other charts, referred to as subcharts, via their dependencies section. When a chart is created for the purpose of grouping together related subcharts/services, such as to compose a whole application or deployment, we call this an umbrella chart.

### 88. How does helm upgrade work?
When a new version of a chart is released, or when you want to change the configuration of your release, you can use the helm upgrade command. An upgrade takes an existing release and upgrades it according to the information you provide.

### 89. Does helm have API?
Helm API. Helmit provides a Go API for managing Helm charts within a Kubernetes cluster. Tests, benchmarks, and simulations can use the Helmit Helm API to configure and install charts to test and query resources within releases.

### 90. What is Helm init?
This is part of helm Version 2. To begin working with Helm, run the ‘helm init’ command: $ helm init. This will install Tiller to your running Kubernetes cluster. It will also set up any necessary local configuration.

### 91. What is value yaml?
The values. yaml file is used to pass values into the Release helm chart. The file contains default parameters that you can override. The values. yaml file is typically located in the folder where you extracted the Release Helm chart zip file.

### 92. What are annotations in Kubernetes?
Annotations allow you to add non-identifying metadata to Kubernetes objects. Examples include phone numbers of persons responsible for the object or tool information for debugging purposes. In short, annotations can hold any kind of information that is useful and can provide context to DevOps teams.

### 93. What are differences between in Hel2 & Helm3?
The major differences are Helm2 and Helm3 are:
- Helm2: Helm2 uses Tiller, a server-side component that was used to keep track of the current state of the Helm release. It doesn't follow 3-Way Strategic Merge Patch, which is also considers old manual changes beside old & new manifests when performing upgrades. 
- Helm3: It doesn't have Tiller anymore and also it performs upgrades using 3-Way Strategic Merge Patch.

