Educates Tutorials
==================

This repository contains a set of workshops for learning about Educates
and for providing a playground which can be used to work on Educates
workshop content.

Prerequisites
-------------

In order to use the workshop you must already have the Educates operator
installed. You need to have cluster admin access for the Kubernetes cluster
to deploy the operator and the workshop.

For installation instructions for the Educates operator see:

* https://github.com/eduk8s/eduk8s

Deployment
----------

To deploy the Educates tutorials run:

```
kubectl apply -k github.com/dsosedov-vmw/eduk8s-test
```

Then run:

```
kubectl get trainingportal/educates-tanzu-labs
```

This will output the URL and login credentials to access the web portal for
the training environment.

Deletion
--------

To delete the training portal deployment, run:

```
kubectl delete -k github.com/dsosedov-vmw/eduk8s-test
```
