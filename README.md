# kubevirt-packer

## Install cni on worker node

```console
kubectl get nodes 
````

returns

```console
NAME                     STATUS   ROLES           AGE   VERSION
kubevirt-control-plane   Ready    control-plane   51m   v1.32.2
```

then

```console
docker exec -it kubevirt-control-plane sh
```

then

```console
cd /tmp
curl -L -o cni-plugins.tgz https://github.com/containernetworking/plugins/releases/download/v1.6.2/cni-plugins-linux-amd64-v1.6.2.tgz
tar -C /opt/cni/bin -xzf cni-plugins.tgz
```

## Deploy multus

```console
kubectl apply -f https://raw.githubusercontent.com/k8snetworkplumbingwg/multus-cni/master/deployments/multus-daemonset-thick.yml
```

## Deploy Kubevirt

```console
kind create cluster --name kubevirt --config=kind_config.yaml
kind delete cluster --name kubevirt

kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/v1.2.2/kubevirt-operator.yaml
kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/v1.2.2/kubevirt-cr.yaml
kubectl create -f https://github.com/kubevirt/containerized-data-importer/releases/download/v1.62.0/cdi-operator.yaml
kubectl create -f https://github.com/kubevirt/containerized-data-importer/releases/download/v1.62.0/cdi-cr.yaml

kubectl create namespace windows2022
kubens windows2022
kubectl apply  -f kubevirt_win2022_dv.yml
kubectl apply  -f kubevirt_win2022_pvc.yml
kubectl apply  -f kubevirt_win2022_vm.yml
kubectl apply  -f kubevirt_win2022_svc.yml

virtctl vnc win2022-vm
```

## CNI

See <https://dev.to/darkedges/kind-wsl2-and-multus-5b9p> for details on configuring a basic CNI instance on WSL2.
