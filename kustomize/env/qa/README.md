# Sample "QA environment" from a base env


Most of the substance here is pulled from ../base/

It tweaks a few minimal things before invoking whatever is defined there.

If you are starting from ground zero, and your own k8s cluster, you can activate this demo
with the following steps

1. You have a working k8s cluster
2. You have already installed the flux CLI
3. You have already run `flux install`
4. You have cloned this repo, and are sitting in this directory
5. [../base/repo.yaml](../base/repo.yaml) has up-to-date information

If you have taken care of all of the above, then all you have left is:

    kubectl apply -k .



When things are reconciled, and the demo webserver is set up, you can see that the webserver
serves the QA contents, rather than the default one from the ppbrown-demo directory.

    Started by Flux CD for QA ENVIRONMENT

It would show "PROD" if you started things from ../prod, and "QA" if from ../qa

NOTE, however, that it uses the same namespace. So you must not try to run both DEV` and 
`PROD` at the same time.

(It IS possible to set up flux to automatically differentiate the namespaces, but I have not done that)

