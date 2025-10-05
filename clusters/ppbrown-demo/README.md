Following the directions at the top level [README.md](/README.md) will have
Flux CD pull in this directory, and automatically create a k8s Deployment 
of nginx, using ClusterIP

This is in the directory path of "clusters/ppbrown-demo", to imply that this
directory could be the top level root configuration for an entire app tree
managed by Flux, in one go.

However, it is perfectly legitimate to also use one-kustomization-per-app type
references in Flux instead.

