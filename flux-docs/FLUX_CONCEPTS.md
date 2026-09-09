# FLUX Concepts (Enterprise Audience)

Previously, I wanted some experience just messing around with basic flux controls.
But when it came time to set up a "proper" Enterprise flux, I was missing some
high level concepts. So here's an orientation

# PRE-REQUISITES

You need to already understand the concept of full GitOps:
The idea that your entire CI/CD pipeline will be fully driven by commits in Git(lab/hub)

# CORE CONCEPTS

You will probably want THREE clumps of git repos. My biggest stumbling block was not
understanding this up front, so I'm making it easier for you to get it.

## 1. The Flux state repo

Flux really wants its OWN REPO, and it needs to have full control over it.
The github token you create for "flux bootstrap" use thus needs full control.

This repo is where it stores its defaut named directory, "flux-system/"

You also probably want to store what might be called "glue" configs here. 
These are the IaC versions of commands like

    flux create source ......
    flux create kustomization ......

You probably want your production/staging/qa environments broken out into subdirs here.

## 2. The Flux deployments repos

These are where you point the above "flux create kustomization ..." calls to.
They are NOT the backend app code repos. They are the places you write the k8s/flux
infrastructure IaC definitions.


## 3. Application code repos

These are the places where devs write the code that generates container images.
You dont even have to care about these. You just need to know where the images get
written to, and that your flux credentials can read them.

You will probably have your flux code scan the container image repos for updates

