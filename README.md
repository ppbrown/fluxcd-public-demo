# fluxcd-public-demo

This is a work in progress, to try out the
k8s based [Flux CD Orchestration tool](https://fluxcd.io/)

# Goal
To allow anyone to point to this repo, and see how Flux CD deploys an application

# Prerequisites
Flux is designed to be CLI based.
(There techinically are GUI wrappers, but at its core, it is CLI, so thats what we will use here)

## 0. Have a working k8s cluster

you need to already have "kubectl" installed, and talking to your k8s cluster as admin

## 1. Install the flux CLI

You need to [install the Flux CLI](https://fluxcd.io/flux/installation/#install-the-flux-cli) by hand.

## 2. Use the CLI to get the flux service up and running

Technically, there are [fancier IaC ways to do this](https://registry.terraform.io/providers/fluxcd/flux/latest).
But the EasyMode(tm) method is to just use

    flux bootstrap github \
     --repository=https://github.com/ppbrown/fluxcd-public-demo \
     --path=clusters/ppbrown-demo

Normally, you would also need to set up github tokens, but this is a PUBLIC repo, you dont have to do that.

## 3. ... profit!

Okay, just kidding. But putting something here temporarily. FYI, I'm not done with the backend, so the above steps
DO NOT ACTUALLY WORK YET.

But in theory, they will in the near future.
