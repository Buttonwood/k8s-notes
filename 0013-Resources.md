### Resources
*	`requests`
* 	`limits`		

```
apiVersion: v1
kind: Pod
metadata:
	name: <pod_name>
spec:
	containers:
		- image: <image_name>/<tag_name>
		  name: <container_name>
		  resources:
		  	requests:
		  		cpu: "500m"
		  		memory: "128Mi"
		  	limits:
		  		cpu: "1000m"
		  		memory: "256Mi"
		  ports:
		  	- containerPort: 8080
		  	  name: http
		  	  protocol: TCP
```
