# Tips for full Flux CD (not this repo)

If this repo has whet your appetite for the real thing... you may get frustrated by the official guide at https://fluxcd.io/flux/get-started/

here's a more new-user-friendly walkthrough for first timers, based on ubuntu.

## Prerequisites

1. you'll need a Kubernetes cluster!  On ubuntu quickstart for 1-node cluster is

    curl -sfL https://get.k3s.io | sh -

But then unfortunately you need to fuss with two layers of kubectl access.
Yes you need both files to keep the future simple for flux cli

    sudo chgrp adm /etc/rancher/k3s/k3s.yaml
    sudo chmod g+r /etc/rancher/k3s/k3s.yaml
    sudo install -D -m 600 -o $(id -u) -g $(id -g) /etc/rancher/k3s/k3s.yaml ~/.kube/config


3. You will need a PRIVATE github repo, for the cluster state. So set one up, but ***Be sure to set visibility as PRIVATE***, not the default public visibility

4. You will need an access token. Official docs say it needs "admin priviledge, minimum". It lies. If you are creating a finegrained token, it needs
(Administration: read/write), PLUS (Contents: read/write)

5. Install the actual flux binary.

    curl -s https://fluxcd.io/install.sh | sudo bash

## Bootstrap install

Run the bootstrap command. For a repo of https://github.com/pbrown/my-flux-cluster you will need to do

    export GITHUB_TOKEN=github_pat_blahBLAHblahBLAHblah
    flux bootstrap github  --owner=ppbrown --repository=my-flux-cluster --token-auth
    # Unless you are working with an 'org' based account you will also need to add
    # --personal

## Success!

If everything went well, then the final lines of output should look like:

    ◎ waiting for Kustomization "flux-system/flux-system" to be reconciled
    ✔ Kustomization reconciled successfully
    ► confirming components are healthy
    ✔ helm-controller: deployment ready
    ✔ kustomize-controller: deployment ready
    ✔ notification-controller: deployment ready
    ✔ source-controller: deployment ready
    ✔ all components are healthy

