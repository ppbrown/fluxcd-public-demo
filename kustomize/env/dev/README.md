# Sample "QA environment" from a base env

This directory is incomplete by itself. It pulls in [../ppbrown-demo](../ppbrown-demo) as a base.
Some people might like to name the base template as literally "base", rather then overriding a normally named one.
Reguardless, to use this one instead of the regular, you can do

    # This works for linux, AND mac
    curl -s https://fluxcd.io/install.sh | sudo bash
    flux install

    flux create source git ppbrown-demo --url=https://github.com/ppbrown/fluxcd-public-demo --branch=main
    kubectl apply -k .
    ## OBSOLETE
    ## flux create kustomization demo-app --source=GitRepository/ppbrown-demo  --path=./clusters/ppbrown-demo --prune=true --interval=1m

Then, when things are reconciled, and the demo webserver is set up, you can see that the webserver serves the QA contents,
rather than the default one from the ppbrown-demo directory.

    Started by Flux CD for QA ENVIRONMENT

NOTE, however, that it uses the same namespace. So you must not try to run both `ppbrown-demo` and `ppbrown-qa` at the same time.

