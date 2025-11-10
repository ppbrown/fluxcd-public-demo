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
4. Deploy app(s) via flux

There are actually two ways you can deploy the demo app. The fastest and
easiest is to deploy directly from my repo, as follows:

    kubectl kustomize https://github.com/ppbrown/fluxcd-public-demo/kustomize/env/dev | kubectl apply -f -
    # That's all, you are now done!

Alternatively, if you want to experiment with actually seeing changes getting
picked up from git, you will want to fork this repo to your own, following
these additional steps:

- Fork the repo.
- Update [../base/repo.yaml](../base/repo.yaml) points to YOUR repo
- Either do the above style kustomize call, or clone your repo, 'cd' to this
  directory, and do `kubectl apply -k .`


Once things are reconciled, and the demo webserver is set up, you can see that the webserver serves the DEV contents, rather than the default one from
the apps/demo-app directory.

>   Started by Flux CD.
>   Special env val = DEV

It would show "PROD" if you started things from [../prod](../prod), and "QA" if from [../qa](../qa)

NOTE, however, that it uses the same k8s namespace. So you must not try to 
run both `DEV` and `PROD` at the same time, for example.

(It IS possible to set up flux to automatically differentiate the namespaces, but I have not done that)


### Reminder on how to tunnel kube service to your desktop:

kubectl -n demo-app  port-forward svc/nginx-service 80
