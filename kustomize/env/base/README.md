# base directory: do not use

This directory is intended to simply be a shared base, for an organization that has multiple
cluster environments, like "prod", "dev",and "qa"

There currently are hooks for a single application, referenced as
app_demo-app.yaml

The structure is designed to make it easy for you to add additional apps under
../apps/newapp
and then add a reference like app_newapp.yaml

After that point, you may then go to the appropriate directory such as
../qa  and run

kubectl apply -k .


