# fluxcd-public-demo

## Purpose

This repo holds EasyMode(tm) demos for the k8s based [Flux CD Orchestration tool](https://fluxcd.io/).
Its target audience is anyone who is new to GitOps, and/or Flux CD.

Flux enables pure "GitOps" driven workflows, 
to manage workloads in a Kubernetes cluster

The existing "Set up Flux for the first time" walkthroughs require that you set up github credentials with special privs for access. 
If you already KNOW you want to use Flux, you should follow the standard setup. 

However, if you aren't sure whether Flux CD is worth the hassle yet, then this demo lets you skip that. With just a few commands from your workstation, you will
be up and running with a Flux-managed demo application in your Kubernetes cluster.

## This repo vs your own

The demo instructions are written so that you can run the demo directly from this repo right here. 
Since it is public, it thereby does not require setting up any github access keys. 

Alternatively, you can choose to fork this repo to one of your own. If you go this route, you may then make changes to
your repo after initial deployment, and then any changes in the repo will get synced to the application(s) running
in your Kubernetes cluster. 

Do note that you will need to keep the fork publically accessible for it to work, unless you go to the extra trouble of setting
up github access credentials.

# Choose your Adventure

There are TWO possible demo paths to choose from. Flux allows use of "direct" kustomization definitions of apps, or use of Helm charts
(or even a mix of both)

The choice of which style to use may be driven by more than just "Do I like/dislike Helm charts?"
Base Flux does not give you much in the way of hand-holding. It does not give you deep diagnostics on 
components that have been deployed (You are expected to use `kubectl` for that).
However, if you have deployed helm under flux, you can use helm for additional visibility. eg

    helm status guestbook --show-resources

You will need to choose between kustomize, or helm, in step 3 below.


# Prerequisites and install steps

Before you go any further, understand that Flux is primarily command line (CLI) based.

There techinically are GUI wrappers for it, but at its core, Flux is CLI based. 
If that makes you uncomfortable, /This is not the guide you are looking for/

## 1. Have a working k8s cluster

Make sure that you already have "kubectl" installed, and talking to your functioning k8s cluster as admin.
It can be a "cluster" of 1 node, for demo purposes, but "kubectl get all" should actually do something useful.

## 2. Install the flux CLI and service

* First, [download the Flux CLI](https://fluxcd.io/flux/installation/#install-the-flux-cli) by hand

* Next, use it to install the Flux service in the cluster.

If you only want to install flux to try it out with this demo, you can just do `flux install`.

If you are interested in keeping the service around for more serious use, `flux bootstrap github` may be more appropriate for you.
This requires creating a github access token for the service.

## 3. Pick your poison

Either of these final install methods should get a demo app up and running for you:

* [Simple app path](clusters/ppbrown-demo/README.md)
* [Helm based deployment](helmbased/README.md)

Once you have it running, changes to the repo will be automatically reflected in the cluster after a small amount of time.

Technically, each of them install different apps, so you can actually do both.

You are now all set up! Poke around, and see how you feel about Flux CD.

---

---

## Random notes about Flux CD

###  This is not Argo CD

There is no special web server that gives you an admin GUI (By default, anyway. You can choose to install an optional third-party web admin GUI though.)

There is no special service port. The flux CLI communicates with the backend using native kubernetes API 
calls, so there's no extra holes in your firewalls to make.

### Removing Flux

To undo all the things flux did in your cluster, first run `flux delete kustomization` on all the things shown by
`flux get kustomizations`. 

You are then clear to simply run `flux uninstall`
