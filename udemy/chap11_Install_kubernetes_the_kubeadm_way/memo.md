# MEMO 
 - just do as https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
 - only init in master node. 
 ```
 kubeadm init --pod-network-cidr=10.244.0.0/16 --apiserver-advertise-address=$masternode_address
 ```
 - only apply pod network(Weave) in master node
 - only join in worker nodes
 - check out image file

## Demo
add demo for virtual box environment from https://github.com/kodekloudhub/certified-kubernetes-administrator-course