# kubevirt-packer

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