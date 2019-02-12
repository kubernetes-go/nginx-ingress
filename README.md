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
```
