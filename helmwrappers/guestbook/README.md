# A helm wrapper to use with Flux CD

The other directory has an example for a single app.
You can make a kustomization file to have multiple apps in one, but
flux wont give the status very well.

However, if you use it with a helmrelease, it will show more depth. 

If you want to use third-party helm charts, use them with a wrapper
as shown in this directory.
Otherwise, if you have written your own Helm charts, use 
"flux create helmrelease ..."

Anyway, to install and run the wrapper in THIS directory, 
do the following

    # If you havent done this command already:
    flux create source git ppbrown-demo \
     --url=https://github.com/ppbrown/fluxcd-public-demo \
     --branch=main --interval=1m
     
    #Now the real thing
    flux create kustomization helmwrapper \
      --source=GitRepository/ppbrown-demo \
      --path=./helmwrappers/guestbook \
      --target-namespace=default \
      --prune=true --interval=1m
