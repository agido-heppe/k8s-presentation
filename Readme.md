# Readme

## Setup

The following packages are required:
- Docker for Desktop
- git
- jq
- curl
- kubectl

## Docker example

```bash
# Clone the demo repository
git clone git@github.com:Ealenn/Echo-Server.git
cd Echo-Server
# Print the content of the dockerfile
cat Dockerfile
# Build an image for the Dockerfile
docker build -t echo-server . -f Dockerfile
# Start the container
docker run -it --rm -d -p 3000:80 echo-server
# Test the container
curl localhost:3000 | jq
```

## Kubernetes exampke

```bash
kubectx arn:aws:eks:eu-west-1:127048123062:cluster/rbp-test-eks-cluster
kubectl apply -f ./deployment/
```

## Kubernetes scaling example

### Scaling the number of pods

```bash
kubectl scale deployment echo-server --replicas=5
```

```bash
while True; do echo curl -s https://echo-server.test.reactivebetting.com/  | jq .host.ip ; done
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