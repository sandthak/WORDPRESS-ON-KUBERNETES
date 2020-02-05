# WORDPRESS on KUBERNETES 

## Requirements:
-	Kubernetes Cluster Setup using kubeadm (1 Master & 1 Worker Nodes)
-	If your Kubernetes setup is not ready, then you have to setup Kubernetes on your local PC or Laptop.
- Here in this setup I have installed Oracle Virtual Box in my laptop and created two VM's and then Installed UBUNTU – 16 VERSION

## DISK/RAM Required:

## Master - Minimum
  2 GB RAM
  2 Cores of CPU

## Slave/ Node - Minimum
  1 GB RAM

# After UBUNTU OS is installed you have to perform the below steps on Both the VM's

## Disable SWAP
 - Execute cmd 'swapoff -a'
 - Comment swap partition in /etc/fstab file and reboot the node
 - Define the static IP  in /etc/network/interfaces
 - Execute  sudo 'apt-get update'
 - Install OpenSSH-Server Package 'apt-get install openssh-server'

## Install DOCKER
 - sudo su
 - apt-get update 
 - apt-get install -y docker.io

## Install APT Transport package and Setting Up repos for KUBERNETES Packages:
- apt-get update && apt-get install -y apt-transport-https curl
- curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
- vim /etc/apt/sources.list.d/kubernetes.list
  deb http://apt.kubernetes.io/ kubernetes-xenial main
- apt-get update

## Install kubeadm, Kubelet And Kubectl
- apt-get install -y kubelet kubeadm kubectl
- vim /etc/systemd/system/kubelet.service.d/10-kubeadm.conf  in Service Section
  Environment=”cgroup-driver=systemd/cgroup-driver=cgroupfs”

## On Kubernetes Master Only
- kubeadm init --apiserver-advertise-address=<IP Address of Kube-Master> --pod-network-cidr=192.168.0.0/16

The above command will throw you two commands Just note down and save it

  ## Commad 1:

  ## Run the commands from the above output as a non-root user
  - mkdir -p $HOME/.kube
  - sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  - sudo chown $(id -u):$(id -g) $HOME/.kube/config

  ## Command 2:
  - kubeadm join 192.168.56.104:6443 --token uln0pz.zcoblbiu2xb0xpnv --discovery-token-ca-cert-hash     sha256:d5f792b8a8a328eb1c278d7c20db2df47cb6e15ea2f1b171b83217f83856c125
  
  
