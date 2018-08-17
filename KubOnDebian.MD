# Getting Started with Kubernetes on Debian

The fast and easy way to get started with Kubernetes - especially if you are running it on baremetal or a vanilla cloud Debian VM instance.  Debian is a great OS to use because it's lightweight, stable, and secure.  You could use this same guide for Ubuntu and it will work the same, Ubuntu is also arguably better for beginners.

### Create VM

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

<img alt="Kub get all nodes" src="https://github.com/kyleziegler/KubernetesGettingStarted/blob/master/img/get_nodes.png" width="300px"/> 

- To view more info on the nodes run 
```
microk8s.kubectl describe nodes
```
![Kub describe nodes](https://github.com/kyleziegler/KubernetesGettingStarted/blob/master/img/describe.png | width=300) 

