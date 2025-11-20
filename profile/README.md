## Purpose

This project is a mlulti-tabs web terminal, that can be embedded in any website. Each tab is connected to the same base VM, but can be connected to nested VM is the base VM has this capability.  
It was developed for online workshops or when following tutorials, but can be used in many other use cases.  
  
This [article](https://www.exoscale.com/blog/multipass/) illustrates the usage of [Multipass](https://multipass.run) nested VM on [Exoscale instances](https://www.exoscale.com)

## Overall Architecture

The following schema is an overview of the architecture.

![Architecture](./images/architecture.png)

The flow is as follows:  

- A user connects to the terminal using his GitHub account
- In the backend a virtual machine is created on the [Exoscale](https://www.exoscale.com) cloud provider
- A multi-tab terminal is returned to the user. Each terminal has a shell connected via SSH to this VM

This project contains the following GitHub repositories:  

- `terminal`: the UI part which, once packaged, can be embedded in a website.
- `instances`: manager in charge of creating Exoscale instances (VM) on demand. This service is developed in Go.
- `wss`: a web socket server which proxies the user input to the underlying VMs. This service is developed in Node.js.
- `auth`: manages user authentication via GitHub. This service is developed in Go.
- `stack`: documentation (still WIP) explaining how to run the application (either locally for testing, and in a Kubernetes cluster).

This application uses:  

- [NATS](https://nats.io) message broker as the communication layer
- Postgres database to store the VMs statuses

## Running it locally

Follow [this documentation (WIP)](https://github.com/w3term/stack) to run the application on your local machine.

## Running it on a Kubernetes cluster

WIP

## Status

This is still a work in progress (even if this terminal is already functional). More documentation and examples will be added soon.