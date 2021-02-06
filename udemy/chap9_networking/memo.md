# MEMO 

## Switching Routing
valid til reset
 - ``ip link`` : list and modify eth(interfaces) on the host
 - ``ip addr`` : see the ip addresses assigned to the interfaces
 - ``ip addr add`` : to set ip addresses on the interfaces
 - ``ip route``,``route`` : view the routing table
 - ``ip route add`` : add entries to the routing table
 - check ``/proc/sys/net/ipv4/ip_forward`` to make sure IP forwarding is enabled on a host(0:unabled,1:enabled)
persist change
 - set IP related entries above in ``/etc/network/interfaces``
 - set IP forwarding in ``/etc/sysctl.conf``
etc
 - ``netstat -nplt`` to get network information(interface,port,route)
 - ``netstat -anp | grep $name`` to get all connection of $name 
 - or ``netsta -natulp`` 

## DNS
 - ``/etc/hosts`` : make host consider hostname as ip address = name resolution
 - ``nameserver`` in ``/etc/resolv.conf`` : address of dns server. if host comes up with unknown hostname, it will look up this server
 - ``search`` in ``/etc/resolv.conf`` :  specify domain name to append
 - in default search ``/etc/hosts`` and then search ``/etc/resolv.conf``
 - ``nslookup`` : query host name from dns server. doesn't consider ``/etc/hosts``

## Namespace
 - ``ip netns add`` : create network namespaces
 - ``ip netns`` : list network namespaces
 - use prefix ``ip netns exec $ns `` to use ``ip link``, ``arp``, ``route``... etc in the namespace.
 ```
 ip netns exec red ip link
 ip -n red link # simpler way
 ```
 - ``ip link add $v-net-0 type bridge``, ``ip link set dev $v-net-0 up`` : create internal bridget network and turn o using "LINUX BRIDGE"
 - connect namespaces using virtual cable, connect namespace to others : check image file 

## Docker Networking
check out docker networking image files

## Container Networking Interface (CNI)
 - docker does not implement CNI, it implements CNM
 - k8s create docker container with "none" network, then invokes CNI plugins by itself

## CNI in K8S
 - cni configuration is declared in ``kubelet.service``. check out the image files

## Weave in K8S
 - ``ps aux | grep kubelet`` to get cni info
 - check ``/etc/cni/`` to find what cni cluster are using
 - just use below command to deploy "Weave" app (you can find this command in k8s document by searching "kubectl apply cloud.weave")
 ```
 kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```
 
### IP Adderess managing in Weave
 - check ``/etc/cni/net.d/net-script.conf`` to configure 