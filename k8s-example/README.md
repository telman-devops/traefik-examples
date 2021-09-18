# Traefik example for kubernetes

### [Step 1] Provision a k8s cluster - using vagrant
Folder vagrant-provisioning
```
cd vagrant-provisioning
vagrant up
```

### [Step 2] Deploy load balancing solution - metallb

* Installation guid [MetalLB](https://metallb.universe.tf/installation/#installation-by-manifest)

* define and deploy a [configmap](https://metallb.universe.tf/configuration/#layer-2-configuration) _(don`t fogot change addresses)_

> More info about MetalLB in lesson [Kube 33.1] 

### [Step 3] Make sure metallb works as expected

```
k create deploy nginx --image nginx
k expose deploy nginx --port 80 --type LoadBalancer
```

After checkout, delete 
```
k delete deploy nginx
k delete svc nginx
```

### [Step 4] Setup dynamic storage provisioning - nfs

* Deploy dynamic NFS provisioning

```
k get sc
# nfs-client
```

> More info about NFS in lesson [Kube 23.1] 

### [Step 5] Install Traefik by Helm chart

[Helm Chart](https://doc.traefik.io/traefik/getting-started/install-traefik/#use-the-helm-chart)

Modify traefik values
```
helm show values traefik/traefik > /tmp/traefik-values.yaml

persistence:
  enabled: true
  name: data
  accessMode: ReadWriteOnce
  size: 128Mi
  path: /data
  annotations: {}
```
Install traefik
```
helm install traefik traefik/traefik --values /tmp/traefik-values.yaml -n traefik --create-namespace
```
Check traefik UI
```
k -n traefik port-forward traefik-*** 9000:9000
```
