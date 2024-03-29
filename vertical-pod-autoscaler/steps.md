```shell
kind create cluster
nix-shell -p openssl
./hack/vpa-up.sh
exit
k apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl patch -n kube-system deployment metrics-server --type=json \
  -p '[{"op":"add","path":"/spec/template/spec/containers/0/args/-","value":"--kubelet-insecure-tls"}]'
k apply -f examples/hamster.yaml
```

Observe VPA and pods
