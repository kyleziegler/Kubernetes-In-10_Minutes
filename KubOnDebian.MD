# Getting Started with Kubernetes on Debian

The fast and easy way to get started with Kubernetes - especially if you are running it on baremetal or a vanilla cloud Debian VM instance.  Debian is a great OS to use because it's lightweight, stable, and secure.  You could use this same guide for Ubuntu and it will work the same, Ubuntu is also arguably better for beginners.

### Create a VM

- Use the cloud vendor of your choice to spin up a vanilla Debian 9 VM.
- I used a simple shared v-core instance with 2gb of ram, plenty for creating an environment to play around with.  I've used Digital Ocean, Google Cloud Platform, and IBM's Cloud and they are all great for this pupose. 

### Installing Kubernetes

1. First we install snapd (package management, universal Linux packages)
```
sudo apt update
sudo apt install snapd
```
2. Once Snap is installed, we add conjure-up (Fast way to deploy software stacks). Docs located here: https://conjure-up.io/
```
sudo snap install conjure-up --classic
```
3. Finally, add kubernetes from the conjure up repo.
```
conjure-up kubernetes
```
4. I chose the microk8s option on the conjure up install, and then restarted my VM

### Installing Lynx
- We'll needs this later for testing our web app in the terminal
```
sudo apt-get update
sudo apt-get install lynx
```

### Getting started with Kubernetes - microk8s

- In this tutorial we are creating one node, so when you run:
```
microk8s.kubectl get no
```

OR

```
microk8s.kubectl get nodes
```

- You should see the name of the machine you are on, in my case: 

<img alt="Kub get all nodes" src="https://github.com/kyleziegler/KubernetesGettingStarted/blob/master/img/get_nodes.png" width="500px"/> 

- To view more info on the nodes run
```
microk8s.kubectl describe nodes
```
<img alt="Kub describe nodes" src="https://github.com/kyleziegler/KubernetesGettingStarted/blob/master/img/describe.png" width="600px"/> 

### Enable the Kubernetes dashboard
- This allows us to view a web UI with statistics on our cluster we'll create.

```
microk8s.enable dns dashboard
```

### Create nginx pods

- Creates 2 pods with the ngninx web server.  Nginx is a simple web server/ reverse proxy, used in LEMP (Linux, Nginx, MySQL, PHP) stacks. 
```
microk8s.kubectl run nginx --image nginx --replicas 2
```
- image here of get all

### Expose the deployment to port 80 

- This allows us to test the app in our browser. 
```
microk8s.kubectl expose deployment nginx --port 80 --target-port 80 --type ClusterIP --selector=run=nginx --name nginx
```

-image here of get all

### Test nginx deployment

```
lynx http://(IP here from the service/nginx ClusterIP)
```

-image here from nginx screen

### Delete deployment 


```
microk8s.kubectl delete deploy/nginx
```

```
microk8s.kubectl delete svc/nginx
```

```
microk8s.kubectl disable dashboard dns
```

- image from get all after deleting

### Congrats!
- You've reached the end of the tutorial, you can now launch web images to a kubernetes cluster, test, view, and delete them. Let me know if there's anything else you'd like to see in this tutorial!
Kyle






