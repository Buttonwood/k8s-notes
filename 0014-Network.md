### Docker network
#### Same Node
*	bridge mode(default)
	*	same IP range
	* 	port forwarding
*	host mode
	*	losing the security
*	container mode
	*	shares a network namespace
	* 	cannot use the same ports

#### Different nodes
*	libnetwork(overlay driver)
* 	weave
*  flannel
*  calico
