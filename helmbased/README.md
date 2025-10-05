# How to use a HELM based Flux CD config

The other top level directory has a trivial example for a single app.
You can make a kustomization file to handle multiple apps but
flux wont give the status of components very well.

However, if you use flux with a helmrelease, it will show more depth. 

This tree currently focuses on using third-party helm charts.
However, you can just as easily use your own local ones.

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
