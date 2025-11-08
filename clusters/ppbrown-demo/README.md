# Purpose
The purpose of this directory is to have Flux CD automatically create a k8s Deployment 
of nginx, using ClusterIP

This is in the directory path of "clusters/ppbrown-demo", to imply that this
directory could be the top level root configuration for an entire app tree
managed by Flux, in one go.

However, it is perfectly legitimate to also use one-kustomization-per-app type
references in Flux instead.

# 0. Prerequisites

As mentioned in the top level [README.md](/README.md), you first need
* A working kubernetes cluster
* The ["flux" CLI tool installed](https://fluxcd.io/flux/installation/#install-the-flux-cli).
* `flux install`

## 1. Define this github repo as a known source

    flux create source git ppbrown-demo --url=https://github.com/ppbrown/fluxcd-public-demo --branch=v1.0-branch

## 2. Define this app as a tracked entity to Flux

    flux create kustomization demo-app --source=GitRepository/ppbrown-demo  --path=./clusters/ppbrown-demo --prune=true --interval=1m

Normally, you would also need to set up github tokens, but this is a PUBLIC repo, so you dont have to do that.

## 3. ... Profit!

Shortly after doing the above, you should then be able to run the diagnostic command below to verify service

    $ flux get kustomizations

    NAME            REVISION                SUSPENDED       READY   MESSAGE
    demo-app    main@sha1:xyzabc      False           True    Applied revision: main@sha1:xyzabc....

Once this is up, standard k8s commands like `kubectl get svc` will show that the new "nginx-service" is running. And if you want to actually see the output from the webserver on your desktop, then one way is the standard port-forward method

    kubectl -n demo-app  port-forward svc/nginx-service 80
    # and now run   YourWebbrower http://localhost
