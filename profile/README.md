## Purpose

This project is a web terminal that can be embedded in any website. It provides multiple Linux terminal which can be very useful when following online workshops / tutorials.

## Overall Architecture

The following diagram is an overview of the microservices architecture of this application.

![Architecture](./images/architecture.png)

In a nutshell:
- a user connects to the terminal using his GitHub account
- in the backend a virtual machine is created on the [Exoscale](https://www.exoscale.com) cloud provider
- this VM leverage the nested virtualization of Exoscale's VM ([read more about nested virtualization](https://www.exoscale.com/syslog/2025-04-01-multipass/))
- a multi-tab terminal is returned to the user. Each terminal has a shell connected via SSH to one of the nested VM

It involves several services:
- web frontend: the one that can be embedded in a website
- a web socket server which proxies the user input to the underlying nested VMs
- an instance manager in charge of creating the VM instances
- a NATS message broker as the communication layer
- a Postgres database that stores the VMs status

## Installation

The backend part can be installed:
- using [Docker Compose](./compose.yml), for local testing
- using Helm, in Kubernetes, for a production environment (more on that soon)

## GitHub application

Before using the application, you need to create a GitHub app to enable GitHub signin.

## Usage

To use w3term in your web application, you only need to add the following snippet in your web page, replacing the placeholders with the details of the GitHub application.

```html
<script src="https://cdn.jsdelivr.net/npm/@web-terminal/terminal@latest/terminal.min.js"></script>
<script>
const terminal = new WebTerminalEmbed({
    githubAppName: 'your-app-name',
    githubClientId: 'your-client-id',
    backendDomain: 'your-domain.com'
});
</script>
```

## Status

WIP: documentation and examples will be added soon 