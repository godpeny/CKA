# MEMO

## ex2
### Security-Context
```
...
securityContext:
      capabilities:
        add: ["NET_ADMIN", "SYS_TIME"]
```
### nslookup Pod Name
 - if ``10.10.10.10.`` is pod ip in default name space, ``nslookup 10-10-10-10.default.pod``

### csr
 - create csr & approve
 - create role (with proper namespace)
 - create rolebinding (with proper namespace)
 - check with ``kubectl auth can-i list secrets --namespace dev --as dave``

## ex3
### Service Account Access
 - create sa
 - create cluster role
 - create cluster role binding
 - ``kubectl describe po`` and check pod's volume is set with secret token with proper name of service account

### jsonpath
 - check cheetsheet

### Network Policy
 - ``kubectl get netpol``, ``kubectl describe netpol xx`` to check current network policy
 - ``nc -z -v -w 2 $svc $port`` in busybox image container to check netpol is set properly.
 ```
 kc exec check -it -- nc -z -v -w 2 np-test-service 80 # check: busybox container pod with sleep command
 ```