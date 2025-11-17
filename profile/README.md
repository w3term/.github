## Purpose

This project is a web terminal that can be embedded in any website. It provides multiple Linux terminal which can be very useful when following online workshops / tutorials.

## Overall Architecture

The following schema is an overview of the architecture.

![Architecture](./images/architecture.png)

The flow is as follows:  

- A user connects to the terminal using his GitHub account
- In the backend a virtual machine is created on the [Exoscale](https://www.exoscale.com) cloud provider
- A multi-tab terminal is returned to the user. Each terminal has a shell connected via SSH to this VM

This project contains the following GitHub repositories:  

- `terminal`: the UI part which, once packaged, can be embedded in a website
- `instances`: manager in charge of creating Exoscale instances (VM) on demand
- `wss`: a web socket server which proxies the user input to the underlying VMs
- `auth`: manages user authentication via GitHub
- `stack`: documentation (still WIP) explaining how to run the application (either locally for testing, and in a Kubernetes cluster).

Under the hood, it also uses NATS message broker as the communication layer and a Postgres database that stores the VMs statuses.

## Status

This is still a work in progress (even if this terminal is already functional). 
Documentation and examples will be added soon.