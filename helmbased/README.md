# How to use a HELM based Flux CD config

The other top level directory has a trivial example for a single app.
You can make a kustomization file to handle multiple apps but
flux wont give the status of components very well.

However, if you use flux with a helmrelease, it will show more depth. 

# WARNING on namespaces

Oddly, while "flux get customizations" works out of the box, "flux get helmreleases"
does not. YOU MUST SPECIFY THE NAMESPACE.

So, for our example here, you will want to use

    flux get helmreleases  -n default

# Usage

This tree currently focuses on using third-party helm charts.
However, you can just as easily use your own local ones.
Additionally, this tree uses Helm-in-github. However, Flux can
also use helm repos directly.

To install this tree's contents within Flux, 
do the following

    # If you havent done this command already:
    flux create source git ppbrown-demo \
     --url=https://github.com/ppbrown/fluxcd-public-demo \
     --branch=main --interval=1m
     
    #Now the real thing
    flux create kustomization helmbased \
      --source=GitRepository/ppbrown-demo \
      --path=./helmbased \
      --prune=true --interval=1m

# Status checks

## Base level Flux check

    $ flux get helmreleases  -n default

    NAME            REVISION        SUSPENDED       READY   MESSAGE
    guestbook       0.1.0           False           True    Helm install succeeded for release default/guestbook.v1 ...

There is also the non-dynamic resource view

    $ flux tree kustomization helmbased
        Kustomization/flux-system/helmbased
    ├── HelmRelease/default/guestbook
    │   ├── Service/default/guestbook-helm-guestbook
    │   └── Deployment/default/guestbook-helm-guestbook
    └── GitRepository/flux-system/argocd-examples


## More detailed check

Since we used helm under the covers, we can then use helm status checks for more details.
When it has fully deployed, you can expect something like the following:

    $ helm status guestbook --show-resources

    NAME: guestbook
    LAST DEPLOYED: Sun Oct  5 18:53:04 2025
    NAMESPACE: default
    STATUS: deployed
    REVISION: 1
    RESOURCES:
    ==> v1/Deployment
    NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
    guestbook-helm-guestbook   1/1     1            1           28m

        ==> v1/Pod(related)
    NAME                                        READY   STATUS    RESTARTS   AGE
    guestbook-helm-guestbook-6c588dc74f-qtxjg   1/1     Running   0          28m

    ==> v1/Service
    NAME                       TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
    guestbook-helm-guestbook   ClusterIP   10.152.183.98   <none>        80/TCP    28m
