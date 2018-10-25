```
kubectl version
kubectl get componentstatuses
kubectl get nodes
kubectl describe nodes {node-1}
kubectl get daemonSets --name-space=kube-system kube-proxy

kubectl get deployments --name-space=kube-system kube-dns
kubectl get services --name-space=kube-system kube-dns

kubectl get deployments --name-space=kube-system kubernetes-dashboard
kubectl get services --name-space=kube-system kubernetes-dashboard
kubectl proxy
```


```
kubectl apply -f obj.yaml
kubectl edit <resource_name> <obj_name>
kubectl delete -f obj.yaml
kubectl delete <resource_name> <obj_name>
```


```
kubectl logs <pod_name>
kubectl exec <pod_name> date
kubectl exec -it <pod_name> --bash
```

### Copying Files to and from Containers
*	Should treat the contents of a container as immutable.
*	It is quicker than building, pushing, and rolling out a new image.

```
kubectl cp <pod_name>:<file_path> <local_file_path>
kubectl cp <local_file_path> <pod_name>:<file_path> 
```

```
kubectl port-forward <pod_name> <port>:<port>
```


### MySQL Singleton
*	A PV(persistent volume)
* 	A Pod(MySQL application)
*	A SV(service expose)

```
vim nfs-volume.yaml

apiVersion: v1
kind: PersistentVolume
metadata:
	name: database
	lables: 
		volume: mysql-volume
spec:
	capacity:
		storage: 1Gi
	nfs:
		server:192.168.0.1
		path: "/exports"

kubectl apply -f nfs-volume.yaml
```

```
vim nfs-volume-claim.yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
	name: database
spec:
	resources:
		requests:
			storage: 1Gi
	selector:
		matchLables:
			volume: mysql-volume
	
kubectl apply -f nfs-volume-claim.yaml
```

```
vim mysql-replicaset.yaml

apiVersion: extensions/v1beta1
kind: ReplicaSet
metadata:
	name: mysql
	lables: 
		app: mysql
spec:
	replicas: 1
	selector:
		matchLables:
			app: mysql
	template:
		metadata:
			lablels:
				app: mysql
		spec:
			containers:
			- name: database
			  image: mysql
			  resources:
			  	requests:
			  		cpu: 1
			  		memory: 2Gi
			  	env:
			  	- name: MYSQL_ROOT_PASSWORD
			  	  value: "123456"
			  	livenessProbe:
			  		tcpScoket:
			  			port: 3306
			  	ports:
			  	- containerPort: 3306
			  	volumeMounts:
			  	 - name: database
			  	   mountPath: "/var/lib/mysql"
			 volumes:
			 	- name: database
			 	  persistentVolumeClaim:
			 	  	claimName: database
```

```
vim mysql-service.yaml
apiVersion: v1
kind: Service
metadata:
	name: mysql
spec:
	ports:
		- port: 3306
		  protocol: TCP
	selector:
		app: mysql
```


## Objects
*	namepsaces(ns)
*	nodes(no)
* 	pods(po)
*	resourcequtotas(quota)

*	configmaps(cm)

*	replicasets(rs)
* 	replicationcontrollers(rc)
*	daemonsets(ds)

*	deployments(deploy)
*	horizontalpodautoscalers(hpa)

*	services(svc)
*	ingress(ing)
*	endpoints(ep)
* 	events(ev)

*	persistentvolumeclaims(pvc)
* 	persistentvolumes(pv)

* 	serviceaccounts(sa)


```
kubectl get ns
kubectl delete svc,deployment -l app=test
kubectl delete pod {pod_name} --grace-period=0 --force
kubectl delete pods -all --namespace test

kubectl explain svc
```

```
kubectl run <deployment_name>  \
--image=<image_name>:<tag_name> \
--env=MYSQL_ROOT_PASSWORD=root \
--port=3306 \
--command -- sh -c "sleep 2" \
--expose \
--replicas=2 \
```


