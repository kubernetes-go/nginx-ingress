# nginx-ingress

## 1. get certs

```sh
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout kube-cluster-domain.key -out kube-cluster-domain.crt -subj "/CN=myhost.io/O=myhost.io"`
```

```sh
kubectl create secret tls tls-secret --key kube-cluster-domain.key --cert kube-cluster-domain.crt
```


```sh
$ sudo cp kube-cluster-domain.crt /usr/local/share/ca-certificates/myhost.io.crt
$ sudo update-ca-certificates
```

```sh
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout registry-domain.key -out registry-domain.crt -subj "/CN=registry.myhost.io/O=registry.myhost.io"`
```

```sh
kubectl create secret tls registry-tls-secret --key registry-domain.key --cert registry-domain.crt
```

```sh
$ sudo cp registry-domain.crt /usr/local/share/ca-certificates/registry.myhost.io.crt
$ sudo update-ca-certificates --fresh
```