# Sample "DEV environment" from a base env


Most of the substance here is pulled from ../base/

It tweaks a few minimal things before invoking whatever is defined there.

If you are starting from ground zero, and your own k8s cluster, you can activate this demo
with the following steps, so long as you have actually checked out this repository,
and are in this directory


    # This works for linux, AND mac
    curl -s https://fluxcd.io/install.sh | sudo bash
    flux install

    ##flux create source git ppbrown-demo --url=https://github.com/ppbrown/fluxcd-public-demo --branch=main

    kubectl apply -k .

Then, when things are reconciled, and the demo webserver is set up, you can see that the webserver
serves the DEV contents, rather than the default one from the ppbrown-demo directory.

    Started by Flux CD for DEV ENVIRONMENT

NOTE, however, that it uses the same namespace. So you must not try to run both DEV` and 
`PROD` at the same time.

(It IS possible to set up flux to automatically differentiate the namespaces, but I have not done that)

