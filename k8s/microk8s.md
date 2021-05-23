## 1. Overview

### What is Kubernetes

[Kubernetes](https://kubernetes.io/) clusters host containerised applications
 in a reliable and scalable way. Having DevOps in mind, Kubernetes makes
 maintenance tasks such as upgrades dead simple.

### What is MicroK8s

[MicroK8s](https://microk8s.io/) is a  [CNCF certified](https://www.cncf.io/certification/software-conformance/) upstream Kubernetes deployment that runs entirely on your workstation or edge device.
 Being a [snap](https://snapcraft.io) it runs all Kubernetes  services natively (i.e. no virtual machines) while packing the entire  set of libraries and binaries needed. Installation is limited by how  fast you can download a couple
 of hundred megabytes and the removal of MicroK8s leaves nothing behind.

### In this tutorial you’ll learn how to…

- Install Homebrew on macOS
- Install Multipass and MicroK8s from Brew
- Run MicroK8s add-ons

### You will only need …

- A machine with macOS with at least 8GB of RAM

## 2. Install Homebrew

Open a terminal and run the installer:

```zsh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

This will download and execute the installer for Homebrew on your Mac.

## 3. Install MicroK8s

With Homebrew installed, you can now use it to install the pre-packaged version
 of MicroK8s. This is achieved in two stages.

First run the command:

```shell
brew install ubuntu/microk8s/microk8s
```

This will download and install a version of Multipass, a VM system for running
 Ubuntu and other packages required by MicroK8s.

The second stage is to initialise the MicroK8s environment, This is done by
 running the `microk8s` command which was added to your system in the
 previous step:

```sh
microk8s install
```

[![asciicast](https://asciinema.org/a/IWhwnidik9xaC2YHfjBUIsLin.svg)](https://asciinema.org/a/IWhwnidik9xaC2YHfjBUIsLin)

## 4. Wait for MicroK8s to start

MicroK8s will run all the components necessary to set up and run a full
 Kubernetes environment. On some systems, this can take a minute or two. We
 can check when the system is ready by running:

```shell
microk8s status --wait-ready
```

## 5. Access Kubernetes

MicroK8s bundles its own version of `kubectl` for accessing Kubernetes. Use it
 to run commands to monitor and control your Kubernetes. For example, to view your node:

```shell
microk8s kubectl get nodes
```

…or to see the running services:

```shell
microk8s kubectl get services
```

## 6. Deploy an app

Of course, Kubernetes is meant for deploying apps and services. You can use
 the kubectl command to do that as with any Kuberenetes. Try
 installing a demo app:

```shell
microk8s kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
```

It may take a minute or two to install, but you can check the status:

```shell
microk8s kubectl get pods
```

## 7. Use add-ons

MicroK8s uses the minimum of components for a pure, lightweight Kubernetes.
 However, plenty of extra features are available with a few keystrokes using
 “add-ons” – pre-packaged components that will provide extra capabilities
 for your Kubernetes, from simple DNS management to machine learning with
 Kubeflow!

To start it is recommended to add DNS management to facilitate communication
 between services. For applications which need storage, the ‘storage’ add-on
 provides directory space on the host. These are easy to set up:

```shell
microk8s enable dns storage
```

## 8. Starting and Stopping MicroK8s

MicroK8s will continue running until you decide to stop it. You can stop and
 start MicroK8s with these simple commands:

```shell
microk8s stop
```

… will stop MicroK8s and its services. You can start again any time by running:

```shell
microk8s start
```

You can also just reinitialise your Kubernetes with  `microk8s reset`.

