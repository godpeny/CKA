# MEMO 

## Json Path In K8S
 - ``kubectl get pods -o=jsonpath='{.}'`` to show info as json format
 - ``[?(@.)]`` for condition
 ```
 $.status.containerStatuses[?(@.name == 'redis-container')].restartCount
 ```
 - ``[*]`` for list all
 - ex1) use sort and column
 ```
 kubectl get pv --sort-by=.spec.capacity.storage -o=custom-columns=NAME:.metadata.name,CAPACITY:.spec.capacity.storage
 ```
 - ex2) get conext where user is ``aws-user`` in ``my-kube-config``
 ```
 kubectl config view --kubeconfig=my-kube-config -o=jsonpath='{.contexts[?(@.context.user == "aws-user")]}'
 ```