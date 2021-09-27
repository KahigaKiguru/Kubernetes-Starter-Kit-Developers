# Day-2 Operations-ready DigitalOcean Kubernetes (DOKS) for Developers

In this tutorial, we provide developers a hands-on introduction on how to get started with an operations-ready Kubernetes cluster on DigitalOcean Kubernetes (DOKS). Kubernetes is easy to set up and developers can use identical tooling and configurations across any cloud. Making Kubernetes operationally ready requires a few more tools to be set up, which are described in this tutorial.

Resources used by the starter kit include the following.
- DigitalOcean droplets (for DOKS cluster)
- DigitalOcean load balancer
- DigitalOcean Block storage for persistent storage
- DigitalOcean Spaces for object storage

Remember to verify and delete the resources at the end of the tutorial, if you no longer need those.


## Operations-ready Setup Overview

Below is a diagram that gives a high-level overview of the setup presented in this tutorial as well as the main steps:

![Setup Overview](res/img/starter_kit_arch_overview.jpg)



# Table of contents

1. [Scope](#scope)
2. [Set up DO Kubernetes](1-setup-DOKS)
3. [Set up DO Container Registry](2-setup-DOCR)
4. [Ingress Using Ambassador](3-setup-ingress-ambassador)
5. [Prometheus Monitoring Stack](4-setup-prometheus-stack)
6. [Logs Aggregation via Loki Stack](5-setup-loki-stack)
7. [Backup Using Velero](6-setup-velero)
8. [Estimate resource usage of starter kit](14-starter-kit-resource-usage)
9. [Automate Everything Using Terraform and Flux](15-automate-with-terraform-flux)


## Scope
This tutorial demonstrates the basic setup you need to be operations-ready.

All the steps are done manually using the command line interface (CLI). If you need end-to-end automation, refer to the last section.

None of the installed tools are exposed using Ingress or load balancer. To access the console for individual tools, we use `kubectl port-forward`.

We will use `brew` (on MacOS) to install the required command-line utilities on our local machine and use the command to work on a DOKS cluster. 

For every service that gets deployed, we will enable metrics and logs. At the end, we will review the `overhead` from all these additional tools and services. That gives an idea of what it takes to be `operations-ready` after your first cluster install. 

This tutorial will use manifest files from this repo. It is recomended to clone this repository to your local environment. The below command can be used to clone this repository.

   ```shell
    git clone https://github.com/digitalocean/Kubernetes-Starter-Kit-Developers.git
    git checkout <BRANCH>   # Use the branch version similar to DOKS, eg. 1.21
   ```
<br><br>

**Notes**
- Use specific branch corresponding to DOKS version (eg. 1.21), when available.
- For this starter kit, we recommend to start with a nodepool of higher capacity nodes (say, 4cpu/8gb RAM) and have 2 nodes. Otherwise, review and allocate node capacity if you run into pods in PENDING state.
- We customize the value files for helm installs of individual components. To get the original value file, use "helm show values". For example: `helm show values prometheus-community/kube-prometheus-stack  --version 17.1.3`.
- There are multiple places where you will change a manifest file to include a secret token for your cluster. Please be mindful of handling the secrets, and do not commit to public git repositories. We've done the due diligence of adding those to .gitignore files.

<br><br>
If you want to automate installation for all the components, refer to [section 15 - Automate with terraform & flux](15-automate-with-terraform-flux).


Go to [Section 1 - Set up DigitalOcean Kubernetes](1-setup-DOKS).

