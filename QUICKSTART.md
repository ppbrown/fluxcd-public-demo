# Quickstart fluxcd demo

Minimal explanation, minimal documentation, just 

"Here's what you need to get a Flux CD demo running in your existing k8s cluster, QUICKLY!"

    # This works for linux, AND mac
    curl -s https://fluxcd.io/install.sh | sudo bash

    flux install
    
    flux create source git ppbrown-demo --url=https://github.com/ppbrown/fluxcd-public-demo --branch=main
    flux create kustomization demo-app --source=GitRepository/ppbrown-demo  --path=./clusters/ppbrown-demo --prune=true --interval=1m

In 60-120 seconds, you should now have a tiny deployment running in the `demo-app` namespace.
Poke around with the usual kubernetes tools of your choice, and/or view the demo output, with

    kubectl -n demo-app  port-forward svc/nginx-service 80
    # and in a different terminal/browser, peek at http://localhost

If you fork this repo to your own (which I encourage, to get full use out of Flux!), dont forget to change `github.com/ppbrown/` to your own repo.

For a more in-depth view of things, go back to the [README](README.md)
