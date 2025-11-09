# Multi-environment use

For people who are very new to Flux or Gitops, you might say to yourself, 
"Okay, the one-shot demo is cool and all, but how do I use flux in multiple
environments (dev/qa/prod) ?"

I have a demo for that too! But I figured the main README was too long, so I split it out to here.

Take a look at [kustomize/env/dev](kustomize/env/dev) to see how you can make a DEV
or other alternative environment that is primarily based on a common "base" environment, overriding just what you need.

There ARE some "official" flux layout examples, at https://github.com/fluxcd/flux2-kustomize-helm-example
However, for many installations, that may be hard to follow, and also massive overkill.
