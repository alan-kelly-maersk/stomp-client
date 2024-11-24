Execute the following commands to automate testing on local kind cluster:

```
kubectl delete -f deploy.yaml
podman exec -it kind-control-plane /usr/local/bin/crictl rmi localhost/stomper:latest
podman build -t stomper:latest .
podman save localhost/stomper:latest -o image.tar
kind load image-archive image.tar
rm image.tar
podman exec -it kind-control-plane /usr/local/bin/crictl images | grep stomper
kubectl apply -f deploy.yaml
kubectl get pods
```
