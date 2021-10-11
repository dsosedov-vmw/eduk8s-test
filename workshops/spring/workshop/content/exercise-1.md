Although the workshop environment is running inside of Kubernetes as a container, it is possible to enable the ability to perform container builds using ``docker``, or other tools that make use of the docker daemon such as ``pack``. This is done using Docker-in-Docker (dind).

Running ``docker`` is the same as if you had it on your local system.

```terminal:execute
command: docker build -t my-nginx-server nginx-files
clear: true
```

The deployment of an image registry per session for use by the user can also be configured. The resulting images from the docker build can be tagged and pushed to the image registry.

```terminal:execute
command: |-
  docker tag my-nginx-server {{registry_host}}/my-nginx-server:latest
  docker push {{registry_host}}/my-nginx-server:latest
```

Kubernetes deployment resource definitions you are using can then be set up to use images from this image registry. The location of the image registry is different per workshop session, so you first need to find the part of the resource definition to change:

```editor:select-matching-text
file: ~/exercises/nginx-sample/deployment.yaml
text: "image: (nginx:.*)"
isRegex: true
group: 1
```

Modify the value for the image location:

```editor:replace-text-selection
file: ~/exercises/nginx-sample/deployment.yaml
text: {{registry_host}}/my-nginx-server:latest
```

Then create the deployment and wait for it to complete:

```terminal:execute
command: |-
  kubectl apply -f nginx-sample
  kubectl rollout status deployment/nginx
```

It can then be accessed:

```terminal:execute
command: curl http://{{session_namespace}}-nginx.{{ingress_domain}}
```

In this example we used a manual step to update the resource definition with the location of the image. It is also possible to include with the workshop scripts which can be run when the workshop session starts, to update such details automatically so a user doesn't need to.
