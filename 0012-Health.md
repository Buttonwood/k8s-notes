

*	Process health check not enough

### Liveness Probe(Determines if an application is running properly)
*	defined per container
*	defined in Pod mainfest
* 	Containers that fail liveness checks are restarted.

```
apiVersion: v1
kind: Pod
metadata:
	name: <pod_name>
spec:
	containers:
		- image: <image_name>/<tag_name>
		  name: <container_name>
		  livenessProbe:
		  	httpGet:
		  		path: <uri_name>
		  		port: <port>
		  	initialDelaySeconds: 5
		  	timeoutSeconds: 1
		  	periodSeconds: 10
		  	failureThreshold: 3
		  ports:
		  	- containerPort: <port>
		  	  name: <>
		  	  protocol: TCP	  		
```

```
kubectl apply -f port-health.yaml
kubectl port-foward <pod_name> <port>:<port>
```


### Readiness Probe(When a container is ready to server user requests)
*	Continers that fail readiness checks are removed from service balancers.


### Types of health checks
*	`httpGet`
* 	`tcpSocket` for databases or other non-HTTP-based APIs
*	`exec`
