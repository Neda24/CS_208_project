# CS_208_project
Comparing data plane & control plane for Docker Containers, QEMU/KVM and Xen VM
Goal: To gain an understanding of Docker containers vs QEMU/kvm and Xen VMs and to compare their data plane and control plane.
Design
Running a Microservices Application, sock shop on

Docker Containers

Docker containerization engine
Docker-compose container orchestration
Used WeaveScope for monitoring
QEMU/ KVM

3 VMs 
1 master node: control plane
2 worker nodes: data plane
Kubernetes orchestration

Xen

Virtual Box
Kubernetes orchestration
Used WeaveScope for monitoring


Selected Sock Shop, a Microservices Demo Application for testing on Docker containers, QEMU/ kvm VMs and Xen VMs.
Implementation on Cloud Labs
Docker Containers
Cloud lab Experiment
Ubuntu-22.04
Dependencies
 curl -sSL https://get.docker.com/ | sh
apt-get install -yq jq python-pip curl unzip build-essential python-dev
curl -o /tmp/terraform.zip https://releases.hashicorp.com/terraform/0.7.11/terraform_0.7.11_linux_amd64.zip
Clone the microservices repo
git clone https://github.com/microservices-demo/microservices-demo
cd microservices-demo
Set up WeaveScope
sudo curl -L git.io/scope -o /usr/local/bin/scope
sudo chmod a+x /usr/local/bin/scope
scope launch
provision the infrastructure
docker-compose -f deploy/docker-compose/docker-compose.yml up -d
provision the infrastructure & simulate user traffic
docker run --net=host weaveworksdemos/load-test -h $frontend-ip[:$port] -r 100 -c 2
docker run --net=host weaveworksdemos/load-test -h $frontend-ip[:$port] -r 100 -c 2
QEMU/kvm
Cloud lab Experiment
Created 3 VMs with kvm small-lan profile: Ubuntu-22.04 
ubuntu-vm0: master node
ubuntu-vm1: worker-1
ubuntu -vm2: worker-2
Created 3 VMs with kvm small-lan profile: Ubuntu-22.04
Set up the master node and worker nodes
 Install Kubernetes Components
Install kubelet, kubeadm, and kubectl
Initialize Kubernetes Master Node. Set up the kubeconfig
Deploy a Pod Network
Join the Worker Nodes
Xen
Every vm had the same microservice installed and tested to ensure correctness and to learn the strengths and weaknesses of each one
We used the sock-shop demo microservice application
We changed as little as possible in of the demo for 2 reason
We wanted to focus setting up the vm environments rather than developing our own application
We want as much consistency between vms
 Github repo link:
https://github.com/microservices-demo/microservices-demo
Demo
Problems faced
Majority of time spent on researching and understanding the problem statement.
Selected a microservice that was deprecated and not supported. 
So many trials and errors for QEMU/kvm since there is no available guide.
Slight difference in different releases cause trouble, so we learned what does not work very well.
The main problem faced through the project was primarily setting up the vm since we had to create our own profiles in order to run each vm
Also, given the security with cloud labs we could not access the front end to test to see if that was working properly. As a result, we chose to use virtual box for the XEN vm to test accessing the microservice through the internet.

References
https://github.com/microservices-demo/microservices-demo?tab=readme-ov-file
https://github.com/weaveworks
https://gloryyusuf20.medium.com/using-the-cloud-to-deploy-a-microservices-application-786d51830815
https://www.n0derunner.com/create-a-linux-vm-with-kvm-in-6-easy-steps/
https://medium.com/@kvihanga/how-to-set-up-a-kubernetes-cluster-on-ubuntu-22-04-lts-433548d9a7d0
https://uthy.hashnode.dev/mastering-kubernetes-setting-up-a-cluster-and-deploying-a-demo-app-with-weaveworks-socks-shop-on-ubuntu-2004


 
