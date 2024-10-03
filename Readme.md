# MiniKube Cluster with Network Overlay Using Cilium

## Start the Minikube Cluster
   ` minikube start

## Check the status
   `minikube status
   
   ![alt text](/home/karthik/p1.png)
   

## Adding new node to the cluster
    `minikube node add

## Display the nodes  
  `kubectl get nodes
  
### Check the status
   `minikube status
   
    ![alt text](/home/karthik/p2.png)


## Install Cilium CLI

```bash
     CILIUM_CLI_VERSION=$(curl -s https://raw.githubusercontent.com/cilium/cilium-cli/main/stable.txt)
     CLI_ARCH=amd64
     if [ "$(uname -m)" = "aarch64" ]; then CLI_ARCH=arm64; fi
     curl -L --fail --remote-name-all https://github.com/cilium/cilium-cli/releases/download/${CILIUM_CLI_VERSION}/cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}
     sha256sum --check cilium-linux-${CLI_ARCH}.tar.gz.sha256sum
     sudo tar xzvfC cilium-linux-${CLI_ARCH}.tar.gz /usr/local/bin
     rm cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}
     
```

## Install Cilium
   `cilium install --version 1.16.2
   
## Validate the Installation
   `cilium status --wait

## Run the connectivity test
    `cilium connectivity test

## Create a deployment 

`kubectl create deployment nginx --image=nginx --replicas=3

### Get all pods in the current namespace
`kubectl get pods -o wide

![alt text](/home/karthik/p3.png)

### Check the connectivity between pods
` kubectl exec -it nginx-676b6c5bbc-7w68m -- curl http://10.0.1.16

![alt text](/home/karthik/p4.png)


## Display the Cilium pods
`kubectl -n kube-system get pods -l k8s-app=cilium

![alt text](/home/karthik/p5.png)

