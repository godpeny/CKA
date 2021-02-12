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
 - Remember 4 fields. ``cacert``, ``cert``, ``key``, ``endpoints`` which are all defined in etcd pod. ``endpoints`` is ``--listen-client-urls``
 - save snapshot ETCD like below 
 ```
etcdctl --cacert="/etc/kubernetes/pki/etcd/ca.crt" --cert="/etc/kubernetes/pki/etcd/server.crt" --key="/etc/kubernetes/pki/etcd/server.key" --endpoints="https://127.0.0.1:2379" snapshot save snapshot.db 
 ```

### Restrore

#### etcd.service
 1. stop ``kube-api`` server
 ```
 service kube-apiserver stop
 ```

 2. restore snapshot in new data directory with ``--data--dir`` option
 ```
 ETCDCTL_API=3 etcdctl snapshot restore snapshot.db --data-dir /var/lib/etcd/backup
 ```

 3. (if etcd.service) config ``etcd.service`` to use new data directory : change ``--data-dir` in ``etcd.service`` to ``/var/lib/etcd/backup``

 4. reload service daemon and restart etcd service
 ```
 systemctl daemon-reload
 service etcd restart
 ```

 5. restart ``kube-api`` server
 ```
 service kube-apiserver start
 ```
#### etcd pod
 1. restore snapshot in new data directory with ``--data--dir`` option
 ```
 ETCDCTL_API=3 etcdctl snapshot restore snapshot.db --data-dir /var/lib/etcd/backup
 ```

 2. (if etcd pod) change ``volumes.hostpath.path`` in ``etcd.yaml`` where name is ``etcd-data`` not ``etcd-cert``!!

check out etcd Docker container on Master node to make sure recovery is completed.