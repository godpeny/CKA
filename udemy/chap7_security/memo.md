# MEMO 
best way to prepare this chapter is to solve practice test and take lecture again 
## TLS
 - https://kubernetes.io/docs/concepts/cluster-administration/certificates/
 - ``openssl x509  -noout -text -in ./server.crt`` to view the certificate 

## Certificate
 - https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/
 - But Edited as below because k8s api version compatibility. Remeber to use ``v1beta1`` and ``usage`` field
```
apiVersion: certificates.k8s.io/v1beta1
kind: CertificateSigningRequest
metadata:
  name: akshay
spec:
  groups:
  - system:authenticated
  request: !@!#...
  usages:
  - client auth
```

## Security Context
 - use below commnad to check ``runAsUser`` is properly set.
```
kc exec ubuntu-sleeper -- whoami
```

## Network Policy
 - Remember to set port to each ``to`` or ``from``