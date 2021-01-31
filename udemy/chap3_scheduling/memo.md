# MEMO

## Manually Assign Pod to Node

 - Use ``nodeName`` field in Pod.Yaml
 - Check out image files

## Create Daemonsets Imperatively in kubectl
 - create deploy as ``--dry-run=client -o yaml`` then change kind to daemonsets  :-0

## Static Pod

- default path : ``/etc/kubernetes/manifests/``
 - there are only static pod. no replicasets, deployments or services.
  
### Check Out Static Pod Path
-  ``systemctl status kubelet`` or ``ps -ef | grep kubelet`` to see the information of kublet on the node

- check out ``kubelet.service``option ``--pod-manifest-path``

- check out ``kubelet.service``option ``--config`` then check config file

## Multiple Schedulers
 - leader election : It is to select leader when multiple copies of same schedulers are running on different nodes. Only one can be active at a time!

### To get multiple schedulers work
 - when single node : set ``--leader-elect=false`` 
 - when multiple master nodes :
```
--leader-elect=true
--lock-object-namespace=<lock-object-namespace>
--lock-object-name=<lock-object-name>
```
    
### Assign pod using custom scheduler
 - add ``schedulerName`` field to Pod.Yaml
 - check pod is assigned by custom-scheduler : ``kubectl get event -o wide -n default`` 