# microk8s

This vagrant file is used to build a pair of Ubuntu based virtual machines that have the MicroK8S setup of Kubernetes.

For development purpose only.

## Prerequisites
- Windows 10
- VirtualBox
- Vagrant

## Installing VirtualBox

In order to install VirtualBox, use this link:

https://www.virtualbox.org/wiki/Downloads

https://download.virtualbox.org/virtualbox/6.1.22/VirtualBox-6.1.22-144080-Win.exe

Install the VirtualBox 6.1.22 Oracle VM VirtualBox Extension Pack as well, using following link:
https://download.virtualbox.org/virtualbox/6.1.22/Oracle_VM_VirtualBox_Extension_Pack-6.1.22.vbox-extpack

## Installing Vagrant

Install Vagrant for Windows

https://www.vagrantup.com/downloads.html

https://releases.hashicorp.com/vagrant/2.2.16/vagrant_2.2.16_x86_64.msi

## Getting Started

The steps to creating the VM for the environment are:
1. Download Git:
    Windows -> https://git-scm.com/download/win
2. Clone this repository:
    - `C:\mkdir Vagrant`
    - `C:\cd Vagrant`
    - `C:\Vagrant\git clone https://github.com/hendraw4n/microk8s.git`
3. Enter the repo directory:
    - `C:\Vagrant\cd microk8s`
4. Start and connect to the VM
    - `C:\Vagrant\microk8s\vagrant up`
    - `C:\Vagrant\microk8s\vagrant ssh`
5. To check that all is up and running, run the following:
```
vagrant@microk8s:~$ kubectl cluster-info
vagrant@microk8s:~$ kubectl get ns
vagrant@microk8s:~$ kubectl get nodes
vagrant@microk8s:~$ kubectl get pods -A
```
7. To stop the VM run `vagrant halt` inside the vagrant folder. 
8. To start a VM from a `Stopped` or `Aborted` state, use `vagrant up`.

## Additional

1. Download the helm packages through the following link:

https://github.com/helm/helm/releases

2. Installing the helm:
   - `vagrant@microk8s:~$ wget https://get.helm.sh/helm-v3.6.2-linux-amd64.tar.gz`
   - `vagrant@microk8s:~$ tar -zxvf helm-v3.6.2-linux-amd64.tar.gz`
   - `vagrant@microk8s:~$ sudo mv linux-amd64/helm /usr/local/bin/helm`
   - `vagrant@microk8s:~$ helm version`

3. Create and installing the Chart:
   - `vagrant@microk8s:~$ kubectl config view --raw >~/.kube/config`
   - `vagrant@microk8s:~$ helm create myapp`
   - `vagrant@microk8s:~$ helm install demo myapp`
   - `vagrant@microk8s:~$ kubectl get pods`

4. Accesing the application:
   - `vagrant@microk8s:~$ export POD_NAME=$(kubectl get pods --namespace default -l"app.kubernetes.io/name=myapp,app.kubernetes.io/instance=demo" -ojsonpath="{.items[0].metadata.name}")`
   - `vagrant@microk8s:~$ kubectl --namespace default port-forward $POD_NAME 8080:80`
   - `vagrant@microk8s:~$ curl http://127.0.0.1:8080`

5. Clean up the release:
   Run the following command
    - `vagrant@microk8s:~$ helm delete demo`
    - `vagrant@microk8s:~$ kubectl get pods`
