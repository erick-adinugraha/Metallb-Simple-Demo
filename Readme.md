# Metallb Demo

## Deploy Metallb
```bash
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.4/config/manifests/metallb-native.yaml
```

## Check the deployed Metallb
```bash
kubectl -n metallb-system get all
```

## Create ip address pools
```bash
kubectl create -f ipaddresspool.yaml
```

## Check the created ip address pools
```bash
kubectl -n metallb-system get ipaddresspool
kubectl -n metallb-system describe ipaddresspool first-pool
```

## Create ip address advertisement
```bash
kubectl create -f l2advertisement.yaml
```

## Check the created ip address advertisement
```bash
kubectl -n metallb-system get l2advertisement
kubectl -n metallb-system describe l2advertisement example
```

## Create deployment and service (load balancer type)
```bash
kubectl create -f deployment.yaml
kubectl create -f loadbalancer.yaml
```

## Access the site
Get the ip address using below command
```bash
kubectl get service/nginx -o=go-template='{{(index .status.loadBalancer.ingress 0).ip}}'
```
Access it at http://{the ip address from above command}