# MEMO 

## Cluster Upgrade
 - just follow https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/

## BackUp ETCD
 - use ``-h`` options in etcdctl.
 - Pre-Setups for convenience
 ```
 export ETCDCTL_API=3
 alias ec=etcdctl
 ```

### Snapshot
 - check out etcd pod on ``kube-system``.
 - rRemember 4 fields. ``cacert``, ``cert``, ``key``, ``endpoints``

### Restrore
 - use ``--data--dir`` option when restore.
 - change ``volumes.hostpath.path`` in ``etcd.yaml`` where name is ``etcd-data`` not ``etcd-cert``!! 
 - check out etcd Docker container on Master node to make sure recovery is completed.
