# MEMO 
 
## Application Failure
 - check service
 - check if service and pod matching
 - check pod

## Controlplane Failure

### Pods
 - check componenet on ``kube-system`` namespace
 - check logs of the pods on ``kube-system`` namespace

### Service
 - ``servicee $component status`` to check status of components. 
 - ``kube-apiserver``, ``kube-controller-manager``, ``kube-scheduler`` on master nodes
 - ``kubelet``, ``kube-proxy`` on worker nodes
 - ``sudo journalctl -u $component`` to see logs of component
 - check static pod path in ``kubelet/config.yaml``. you can find the path in ``kubelet.service.d/kubeadm.conf``

## Worker Node Failure
 - ``top`` to check cpu usage
 - ``df -h`` to check disk usage
 - ``service kubelet status`` to check kubelet and ``sudo journalctl -u kubelet`` to see logs of kubelet
 - ``openssl x509  -noout -text -in /var/lib/kubelet/worker-1.crt`` to check certification
 - ``kubectl cluster-info`` to check api server ip:port

## Network
 - check cni (Weave) is installed
 - check kube-proxy logs and configmap
 - ``kubectl get ep -n kube-system`` to check ``core-dns`` service has endpoint.