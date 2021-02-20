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