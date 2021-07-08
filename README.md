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

The steps to creating the VM for the local DEV environment are:
1. Download Git:
    Windows -> https://git-scm.com/download/win
2. Clone this repository:
    - `C:\mkdir Vagrant`
    - `C:\cd Vagrant`
    - `C:\Vagrant\git clone https://github.com/hendraw4n/microk8s.git`
3. Enter the repo directory:
    - `C:\Vagrant\cd microk8s`
4. Run `C:\Vagrant\microk8s\vagrant up`
5. Run `C:\Vagrant\microk8s\vagrant ssh`
6. To check that all is up and running you should run:
```
$ kubectl cluster-info
$ kubectl get ns
$ kubectl get nodes
$ kubectl get pods -A
```

7. Run `kubectl config view --raw >~/.kube/config`
8. To stop the VM run `vagrant halt` inside the vagrant folder. 
9. To start a VM from a `Stopped` or `Aborted` state, use `vagrant up`.
