# Kubernetes

[https://gist.github.com/ipedrazas/95391ffd88190bea94ca188d3d2c1cbe](https://gist.github.com/ipedrazas/95391ffd88190bea94ca188d3d2c1cbe)

#### Different kubecluster

```bash
$ kubectl --kubeconfig=kubeconfig-path get ing
```

#### Forward Port

```bash
# Forward port of Pod to your local machine
kubectl port-forward <podname> <local-and-remote-port> 
# Forward port to service
kubectl port-forward <servicename> <port> 
```

#### Grep by name

```bash
kubectl get ing | grep ing-name | awk 'BEGIN { ORS="" }; { print $1 };'
```

###### Bash Script

```bash 
# Get kubectl with grep
kbctl() {
  kubectl get $1 | grep $2
}
```

#### Create TLS Secret

```bash
kubectl create secret tls secret-name --cert=cert.crt --key=dec.key
```