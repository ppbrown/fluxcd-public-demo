# fluxcd-public-demo

This is a work in progress, to try out the
k8s based [Flux CD Orchestration tool](https://fluxcd.io/)

# Goal
To allow anyone to point to this repo, and see how Flux CD deploys an application

# Prerequisites and install steps

Before you go any further, understnad that Flux is primarily command line (CLI) based.

There techinically are GUI wrappers for it, but at its core, it is CLI based. 
If that makes you uncomfortable, /This is not the guide you are looking for/

## 0. Have a working k8s cluster

Make sure that you need to already have "kubectl" installed, and talking to your functioning k8s cluster as admin.
It can be a "cluster" of 1 node, for demo purposes. But "kubectl get all" should actually do something useful.

## 1. Install the flux CLI

You need to [install the Flux CLI](https://fluxcd.io/flux/installation/#install-the-flux-cli) by hand.

## 2. Use the CLI to get the flux service up and running

Technically, there are [fancier IaC ways to do this](https://registry.terraform.io/providers/fluxcd/flux/latest).
But the EasyMode(tm) method is to just use

    flux install

    flux create source git ppbrown-demo \
     --url=https://github.com/ppbrown/fluxcd-public-demo \
     --branch=main --interval=1m

    flux create kustomization demo-cluster \
     --source=GitRepository/ppbrown-demo \
     --path=./clusters/ppbrown-demo \
     --prune=true --interval=1m



Normally, you would also need to set up github tokens, but this is a PUBLIC repo, so you dont have to do that.

## 3. ... Profit!

Okay, just kidding. But putting something here temporarily. FYI, I'm not done with the backend, so the above steps
DO NOT DO ANYTHING YET.

But in theory, they will in the near future.
