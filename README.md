# nginx-ingress

## 1. get certs

```sh
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout kube-cluster-domain.key -out kube-cluster-domain.crt -subj "/CN=myhost.io/O=myhost.io"
```

## 2. install it on Kubernetes

```sh
$ kubectl create secret tls tls-secret --key kube-cluster-domain.key --cert kube-cluster-domain.crt
```

## 3. install nginx ingress

### 3.1 git clone this repo and run at root folder

```sh
$ kubectl apply -f nginx.oneclick.yaml
```

### 3.2 install from raw

```sh
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes-go/nginx-ingress/master/nginx.oneclick.yaml
```


## 4. access from local

```sh
$ sudo cp kube-cluster-domain.crt /usr/local/share/ca-certificates/myhost.io.crt
$ sudo update-ca-certificates --fresh
$ curl https://myhost.io
```


## 5. access externally

```sh
$ kubectl get svc | grep nginx

> nginx-ingress   NodePort    10.96.185.164   <none>        80:32323/TCP,443:31585/TCP   3h4m

$ kubectl port-forward svc/nginx-ingress 80:80
$ kubectl port-forward svc/nginx-ingress 443:443
```