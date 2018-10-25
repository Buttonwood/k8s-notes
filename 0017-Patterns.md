### Single-node, multiple-container application pattern
#### Sidecar
*	A main container and a sidecat container
*	Containers on the same node are able to share a local disk volume.

![](img/0057.png)

#### Adapter
*	provide a unified interface for aggregating(pods or containers)
 
![](img/0058.png)
