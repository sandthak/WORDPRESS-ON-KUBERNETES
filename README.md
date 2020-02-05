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
- cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
  deb http://apt.kubernetes.io/ kubernetes-xenial main
  EOF
- apt-get update

## Install kubeadm, Kubelet And Kubectl
- apt-get install -y kubelet kubeadm kubectl
- vim /etc/systemd/system/kubelet.service.d/10-kubeadm.conf in [Service Section]
  Environment=”cgroup-driver=systemd/cgroup-driver=cgroupfs”
- 
