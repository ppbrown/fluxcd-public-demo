# fluxcd-public-demo

This is repo holds EasyMode(tm) demos for the k8s based [Flux CD Orchestration tool](https://fluxcd.io/)

(If you haven't heard of Flux before, it is superficially similar to Argo CD)

There are a lack of simple straightforward demos for Flux at present, so I created this repo.
My hope is that anyone can use this repo to quickly and easily start up a trivial little
kubernetes hosted demo application, to get a feel for Flux with a minimum of effort.

Technically, there are [fancier IaC ways to do some of the setup steps](https://registry.terraform.io/providers/fluxcd/flux/latest).
But I'm focusing on EasyMode(tm) for beginner puprposes.

# Choose your Adventure

There are now TWO possible demo paths to choose from.
Flux allows use of "direct" kustomization definitions of apps, or use of Helm charts
(or even both, but we dont need to go into that here)

This choice may be driven by more than just "Do I like/dislike Helm charts?"

Base Flux does not give you much in the way of hand-holding. It does not give you deep diagnostics on 
components that have been deployed (You are expected to use `kubectl`)
However, if you have deployed helm under flux, you can then use things like

    helm status guestbook --show-resources


# Prerequisites and install steps

Before you go any further, understand that Flux is primarily command line (CLI) based.

There techinically are GUI wrappers for it, but at its core, Flux is CLI based. 
If that makes you uncomfortable, /This is not the guide you are looking for/

## 1. Have a working k8s cluster

Make sure that you need to already have "kubectl" installed, and talking to your functioning k8s cluster as admin.
It can be a "cluster" of 1 node, for demo purposes. But "kubectl get all" should actually do something useful.

## 2. Install the flux CLI

You need to [install the Flux CLI](https://fluxcd.io/flux/installation/#install-the-flux-cli) by hand.

## 3. Pick your poison

* [Simple app path](clusters/ppbrown-demo/README.md)
* [Helm based deployment](helmbased/README.md)



# Random notes about Flux CD

##  This is not Argo CD

There is no special web server.

There is no special service port.

The flux CLI communicates with the backend using native kubernetes API calls. So there's no extra holes in your firewalls to make.

