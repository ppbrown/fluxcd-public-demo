# Quickstart fluxcd demo

Minimal explanation, minimal documentation, just 

"Here's what you need to get a Flux CD demo running in your existing k8s cluster, QUICKLY!"

    # This works for linux, AND mac
    curl -s https://fluxcd.io/install.sh | sudo bash

    flux install
    
    flux create source git demo-app --url=https://github.com/ppbrown/fluxcd-public-demo --branch=main
    flux create kustomization demo-app --source=GitRepository/demo-app  --path=./kustomize/apps/demo-app --prune=true --interval=1m

In 60-120 seconds, you should now have a tiny deployment running in the `demo-app` namespace.
Poke around with the usual kubernetes tools of your choice, and/or view the demo output, with

    kubectl -n demo-app  port-forward svc/nginx-service 80
    # and in a different terminal/browser, peek at http://localhost

You may notice that the output looks a little strange. It has `${FLUX_ENV_NAME}`

This is because this demo has two ways to run. You picked the quick-and-simple way.
But if you want to see the proper enterprise way of doing things, do 
`flux delete kustomization demo-app; flux uninstall` and
start again from [kustomize/env/dev](kustomize/env/dev)


If you fork this repo to your own (which I encourage, to get full use out of Flux!), 
dont forget to change all references of `github.com/ppbrown/` to your own repo,
and update --branch if appropriate

For a more in-depth view of things, go back to the [README](README.md)
