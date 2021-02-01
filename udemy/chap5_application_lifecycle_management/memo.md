# MEMO 

## Docker 'CMD' vs 'ENTRYPOINT'
 - entrypoint : command that is run at startup
 - cmd : default parameter passed to the command
 - check out image files 1,2

## K8S Yaml
 - command : override 'ENTRYPOINT' instruction in the Dockerfile
 - args : override 'CMD' instruction in the Dockerfile

## ConfigMap and Secrets
 - ``envFrom``

### Configmaps
  - ``configmapRef``

### Secrets
 - imperative way is more convenient. In Declarative way, you need encode variables. (Check out image file)
