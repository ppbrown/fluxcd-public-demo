# Sample "DEV environment" from a base env

This is an example of how you can support multiple environments from a mostly shared common source tree.
There are many other, more complex possible ways to handle it. This layout is a nice middle ground
between flexbility, and being easy to understand.

Most of the substance here is pulled from `../base` .
It tweaks a few minimal things before applying the code. 

If you are starting from ground zero, and your own k8s cluster, you can activate this demo
with the following steps

1. Have a working k8s cluster
2. Install the flux CLI ( `curl -s https://fluxcd.io/install.sh | sudo bash` )
3. Run `flux install`
4. Clone this repo, and cd to this directory
5. Ensure [../base/repo.yaml](../base/repo.yaml) has up-to-date information

If you have taken care of all of the above, then all you have left to do is:

    kubectl apply -k .



Once things are reconciled, and the demo webserver is set up, you can see that the webserver
serves the DEV contents, rather than the default one from the apps/demo-app directory.

    Started by Flux CD.
    Special env val = DEV

It would show "PROD" if you started things from [../prod](../prod), and "QA" if from [../qa](../qa)

NOTE, however, that it uses the same namespace. So you must not try to run both `DEV` and 
`PROD` at the same time, for example.

(It IS possible to set up flux to automatically differentiate the namespaces, but I have not done that)

## Full GitOps

Remember that the configuration is set to pull from `github.com/ppbrown`, not your local clone of the repo. So if you want
to see actual "GitOps" dynamic updates in action, you will need to fork the repo,
and update [../base/repo.yaml](../base/repo.yaml) before running.

