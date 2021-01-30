# MEMO 
- --dry-run: By default as soon as the command is run, the resource will be created. If you simply want to test your command, use the --dry-run=client option. This will not create the resource, instead, tell you whether the resource can be created and if your command is right.

- -o yaml: This will output the resource definition in YAML format on the screen.

## POD
 - Create an NGINX Pod
```
kubectl run nginx --image=nginx
```
 - Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)

```
kubectl run nginx --image=nginx  --dry-run=client -o yaml
```

## Deployment
 - Create a deployment
```
kubectl create deployment --image=nginx nginx
```
 - Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)
```
kubectl create deployment --image=nginx nginx --dry-run -o yaml
```
 - Generate Deployment with 4 Replicas
```
kubectl create deployment nginx --image=nginx --replicas=4
```

 - You can also scale a deployment using the kubectl scale command.
```
kubectl scale deployment nginx --replicas=4
```
- Another way to do this is to save the YAML definition to a file. You can then update the YAML file with the replicas or any other field before creating the deployment.

```
kubectl create deployment nginx --image=nginx--dry-run=client -o yaml > nginx-deployment.yaml
```

## Service
 - Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379 
 - (This will automatically use the pod's labels as selectors)
```
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
```
 - OR 
 - (This will not use the pods labels as selectors, instead it will assume selectors as app=redis. You cannot pass in selectors as an option. So it does not work very well if your pod has a different label set. So generate the file and modify the selectors before creating the service)
```
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml
```
 - Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes:
 - (This will automatically use the pod's labels as selectors, but you cannot specify the node port. You have to generate a definition file and then add the node port in manually before creating the service with the pod.)
```
kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml
```
 - Or
 - (This will not use the pods labels as selectors)
```
kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
```
 - Both the above commands have their own challenges. While one of it cannot accept a selector the other cannot accept a node port. I would recommend going with the `kubectl expose` command. If you need to specify a node port, generate a definition file using the same command and manually input the nodeport before creating the service.