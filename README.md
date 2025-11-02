# fluxcd-public-demo

## Purpose

This repo holds EasyMode(tm) demos for the k8s based [Flux CD Orchestration tool](https://fluxcd.io/).
Its target audience is anyone who is new to GitOps, and/or Flux CD.

(If you haven't heard of Flux before, it is superficially similar to Argo CD, in that it enables pure "GitOps" workflows
to manage workloads in a Kubernetes cluster)

The existing "Set up Flux for the first time"
walkthroughs require that you set up github credentials with special privs for access. 
If you already KNOW you want to use Flux, you should follow the standard
setup. However, if you aren't sure whether Flux CD suits your style, then this demo is for you.

## Source location choice - this repo

The demo instructions are written so that you can run the demo directly from this repo right here. 
Since it is public, it thereby does not require setting up any github access keys. 
In an way, it is similar to running a public helm chart. It will set up the demo app for you with a minimum of fuss.

The app should fully come up this way, and you will be able to poke around and see what things look like running under Flux CD.
You will not be able to make changes in proper gitops style, however, unless you choose to do the setup from a clone of this repo.

## Source location choice - clone to your repo

Alternatively, you can choose to clone this repo to one of your own. If you go this route, you may then make changes to
your repo after initial deployment, and then any changes in the repo will get synced to the application(s) running
in your Kubernetes cluster. 

Do note that you will need to keep the clone publically accessible for it to work, unless you go to the extra trouble of setting
up github access credentials.

# Choose your Adventure

There are now TWO possible demo paths to choose from. The same app is deployed, but via slightly different framework.

Flux allows use of "direct" kustomization definitions of apps, or use of Helm charts
(or even both, but we dont need to go into that here)

The choice of which style to use may be driven by more than just "Do I like/dislike Helm charts?"
Base Flux does not give you much in the way of hand-holding. It does not give you deep diagnostics on 
components that have been deployed (You are expected to use `kubectl` for that).
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

Either of these final install methods should get the demo up and running for you:

* [Simple app path](clusters/ppbrown-demo/README.md)
* [Helm based deployment](helmbased/README.md)

Once you have it running, changes to the repo will be automatically reflected in the cluster after a small amount of time.


# Random notes about Flux CD

##  This is not Argo CD

There is no special web server (By default, anyway. You can choose to add optional web layers though.)

There is no special service port.

The flux CLI communicates with the backend using native kubernetes API calls. So there's no extra holes in your firewalls to make.

