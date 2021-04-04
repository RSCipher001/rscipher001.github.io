+++
categories = ["kubernetes", "cloud_computing"]
date = "2021-04-04"
description = "How can we install and start using Kubernetes in Ubuntu and derivatives using MiniKube, this can also be used as reference for other Linux variants like RedHat, Fedora, SUSE, etc."
title = "Kubernetes in Ubuntu with Minikube"
+++

I am skipping introduction part for **Kubernetes** and **Docker**, you can read that everywhere on the Internet. Let’s talk about **Minikube**.

> **Minikube** runs a single-node **Kubernetes** cluster inside a VM on your laptop for users looking to try out **Kubernetes** or develop with it day-to-day.

It says **Minikube** allow us to run **Kubernetes** cluster on our Desktop or Laptop using virtual machine for learning. **Minikube** can run on any virtual machine technology like virtual-box, kvm, vmware, etc. It can also use our host OS instead VM. In this tutorial I will use VirtualBox. Understanding **Kubernetes** is tough in the beginning because of terminology (jargons) but don’t worry it is very easy when you take one step at a time, trust me you are going to love it and by the way you need minimum 8 GB RAM for smooth experience. We are going to take following steps

- Install **Minikube** and `kubectl`.
- Install VirtualBox and VirtualBox Extensions.
- Write an hello-world application in NodeJS.
- Create a Docker image for our applications.
- Create a **Kubernetes** deployment.
- Create a **Kubernetes** service.
- And you'll be ready to explore **Kubernetes**.


## First Step: Installation

We need to install `kubectl` and **Minikube**. `kubectl` is a command line program which is used to do almost everything in **Kubernetes** cluster, you can install it using `snap` but it caused some problems for me because I didn't install with classic flag and I didn’t try `snap` again. You can [click here](https://kubernetes.io/docs/tasks/tools/install-kubectl/) for official installation instruction. Anyways here are quick copy paste from their GitHub README, it is the fastest and best way to install both `kubectl` and **Minikube**

#### **Minikube**
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo cp minikube /usr/local/bin/ && rm minikube
```

#### kubectl
```
curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x kubectl && sudo cp kubectl /usr/local/bin/ && rm kubectl
```

You can verify successful installation using `kubectl version` and `minikube version`

```
=> minikube version
minikube version: v0.30.0

=> kubectl version
Client Version: version.Info{Major:"1", Minor:"12", GitVersion:"v1.12.2", GitCommit:"17c77c7898218073f14c8d573582e8d2313dc740", GitTreeState:"clean", BuildDate:"2018-10-24T06:54:59Z", GoVersion:"go1.10.4", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.0", GitCommit:"fc32d2f3698e36b93322a3465f63a14e9f0eaead", GitTreeState:"clean", BuildDate:"2018-03-26T16:44:10Z", GoVersion:"go1.9.3", Compiler:"gc", Platform:"linux/amd64"}
```


## Preparation: Install VirtualBox

**Minikube** uses VirtualBox so install VirtualBox using `sudo apt install VirtualBox-qt VirtualBox-ext-pack` and accept ToC prompt during installation.


## Running **Minikube**

Open terminal and type `minikube start` and it will start minikube. **Minikube** downloads few files on first run so it is going to take some. It may take up-to 10 minutes or more on slow systems.

```
$ minikube start
Starting local Kubernetes v1.10.0 cluster...
Starting VM...
Getting VM IP address...
Moving files into cluster...
Setting up certs...
Connecting to cluster...
Setting up kubeconfig...
Starting cluster components...
kubectl is now configured to use the cluster.
Loading cached images from config file.
```

Minikube is **Kubernetes** cluster which is up and running.


### Useful Information About Minikube

- **Minikube** creates a virtual machines using headless VirtualBox.
- It downloads temporary files in `$HOME/.minikube/cache/` folder.
- **Minikube** virtual machine related files can be found in `$HOME/.minikube/machines/minikube/`
- You can also verify **Minikube** VM installation by opening VirtualBox, it will show minikube in the VM List.


## Let's play jargon games

Every time I read a **Kubernetes** tutorial I found everything confusing because of words like pods, deployment, service, NodePort, etc. This is when most people gets confused and runs away. Let’s avoid that by familiarizing ourself with **Kubernetes** terminology. I assume you're already familiar with Docker terminology and have basic knowledge of docker and Dockerfile. You can access official glossary [here](https://kubernetes.io/docs/reference/glossary/). We need to understand about Pods, Deployments and services to get started, When you'll a have a clear idea about these three you can learn everything on your own.

#### Pod

Pods are very fundamental element in **Kubernetes**. Official documentation has the following definition.
> The smallest and simplest **Kubernetes** object. A Pod represents a set of running containers on your cluster.

> A Pod is typically set up to run a single primary container. It can also run optional sidecar containers that add supplementary features like logging. Pods are commonly managed by a Deployment.

First of all ignore that deployment word if you don't know what it means, we will learn about everything. 

A pod is either a single container or a collection of tightly coupled containers that can't work without each other.

#### Cluster

> A set of machines, called nodes, that run containerized applications managed by **Kubernetes**.

> A cluster has several worker nodes and at least one master node.

It should be clear by reading above definition, cluster is a set of machines that runs containerized applications that is controlled/managed by **Kubernetes**. For simplification think about **Minikube** because **Minikube** is a cluster or in this case **Minikube** is a **Kubernetes** cluster.

#### Deployment

> An API object that manages a replicated application.

Deployment is a **Kubernetes** object, Deployment is created from container images, you can deploy a docker image as a deployment. 

For example your app is packed in a docker image named `your-app:v1`, to run your app in **Kubernetes** you can create a deployment using this image and name it `your-app` or whatever you like, this will create a **Kubernetes** deployment and now you can play with your application using **Kubernetes**. To run your application **Kubernetes** will create one or more pods those pods will contain one or more containers that runs your application. When you create a deployment.

#### Service

> An API object that describes how to access applications, such as a set of Pods , and can describe ports and load-balancers.

We use deployment to run our application in **Kubernetes** but we can't access it outside the pods. To expose a service outside it's pod we use a Service. Creating a service will expose a deployment to the world and everyone can access the service. Service is also a **Kubernetes** object, you can interact with all **Kubernetes** objects using **Kubernetes** REST API which allow us to automate tasks easily.

If you're still confused then take some time, 

#### Let's create Docker Image
We need to deply something to **Minikube** so I am following Hello **Minikube** tutorial from their official tutorials. In this step we will create an image from Dockerfile and then deploy that image on **Kubernetes**.


**File: Dockerfile**
```Dockerfile
FROM node:6.14.2
EXPOSE 8080
COPY server.js .
CMD node server.js
```

**File: server.js**
```js
var http = require('http');

var handleRequest = function(request, response) {
  console.log('Received request for URL: ' + request.url);
  response.writeHead(200);
  response.end('Hello World!');
};
var www = http.createServer(handleRequest);
www.listen(8080);
```

```bash
docker build -t hello_node:v1 .
```

appending `:v#` is common practice for memorizing versions where `#` is version number.

Now you can check your images by command `docker images` or `docker image ls`

Now it is time to play with ``Kubernetes``.

To be continued...

## Other Resources
- [**Minikube**: GitHub](https://github.com/kubernetes/minikube) <br>
- [**Kubernetes**: GitHub](https://github.com/kubernetes/kubernetes) <br>
- [**Hello Minikube**](https://kubernetes.io/docs/tutorials/hello-minikube) <br>