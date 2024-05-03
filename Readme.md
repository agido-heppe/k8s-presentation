# Readme

## Setup

The following packages are required:
- [Docker for Desktop](https://www.docker.com/products/docker-desktop/)
- git
- jq
- curl
- kubectl

```bash
brew install git jq curl kubectl
```

## Docker example

Visit https://github.com/Ealenn/Echo-Server.

```bash
# Clone the demo repository
git clone git@github.com:Ealenn/Echo-Server.git
cd Echo-Server
# Print the content of the dockerfile
cat Dockerfile
# Build an image for the Dockerfile
docker build -t echo-server . -f Dockerfile
# Start the container
  docker run -it --name echo-server -v /tmp/:/mnt/host_tmp/ --rm -d -p 3000:80 echo-server
# Test the container
curl localhost:3000 | jq
```

## Kubernetes exampke

### Deployment
```bash
kubectx docker-desktop
kubectx arn:aws:eks:eu-west-1:127048123062:cluster/rbp-test-eks-cluster
kubectl create namespace echo-server
kubectl --namespace echo-server apply -f ./deployment/
```

### Inspection

```
watch -n1 kubectl -n echo-server get pods -o wide
```

### Scaling example the number of pods

```bash
kubectl patch deployment echoserver --patch-file patches/patch-horizontal.yaml
```

### Vertical scaling

```bash
kubectl patch deployment echoserver --patch-file patches/patch-vertical.yaml
```

### Cleanup
```bash
kubectl --namespace echo-server delete -f ./deployment/
kubectl delete namespace echo-server
```



```bash
while True; do curl -s https://echo-server.test.reactivebetting.com/  | jq .host.ip ; done
```


### Scaling the resource requests to scale nodes

Adjust resources and reapply
```
        resources:
          limits:
            memory: 6G
            cpu: 250m
          requests:
            memory: 6G
            cpu: 250m
```

Show pods
```
~/go/bin/eks-node-viewer --resources=cpu,memory
```

## ArgoCD Demo

https://github.com/agido-heppe/argocd-demo
