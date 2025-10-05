# fluxcd-public-demo

This is repo is a demo for the k8s based [Flux CD Orchestration tool](https://fluxcd.io/)

(It is superficially similar to Argo CD in some ways, if you have heard of that, but not Flux)

There are a lack of simple straightforward walkthroughs, so I created this repo as a demo.
Anyone can use this repo to quickly and easily start up a trivial little
kubernetes hosted demo application, to see how Flux CD deploys an application

# Prerequisites and install steps

Before you go any further, understand that Flux is primarily command line (CLI) based.

There techinically are GUI wrappers for it, but at its core, Flux is CLI based. 
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

The above steps now work!

The diagnostic command below should eventually show you something like the following:

    $ flux get kustomizations

    NAME            REVISION                SUSPENDED       READY   MESSAGE
    demo-cluster    main@sha1:4a72b38e      False           True    Applied revision: main@sha1:xyzabc....
