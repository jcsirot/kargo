Kargo's roadmap
=================

### Self deployment (pull-mode)
- the playbook would install and configure docker and the etcd cluster
- the following data would be inserted into etcd: certs,tokens,users,inventory,group_vars.
- a "kubespray" container would be deployed (kargo-cli, ansible-playbook, kpm)
- to be discussed, a way to provide the inventory
- self deployment of the node

### Provisionning and cloud providers
- Terraform to provision instances on GCE, AWS, Openstack, Digital Ocean, Azure
- On AWS autoscaling, multi AZ, multi-region (Ubernetes)
- On Azure autoscaling, create loadbalancer 
- On GCE be able to create a loadbalancer automatically (IAM ?)
- TLS boostrap support for kubelet 
  (related issues: https://github.com/kubernetes/kubernetes/pull/20439 <br>
   https://github.com/kubernetes/kubernetes/issues/18112)

### Tests
- Run kubernetes e2e tests
- CI Tests for CoreOS (CentOS Support = requirements for us)
- migrate to jenkins
(a test is currently a deployment on a 3 node cluste, testing k8s api, ping between 2 pods)
- Full tests on GCE per day (All OS's, all network plugins)
- trigger a single test per pull request
- single test with the Ansible version n-1 per day
- Test idempotency on on single OS but for all network plugins/container engines
- single test on AWS per day
- test different achitectures : 
           - 3 instances, 3 are members of the etcd cluster, 2 of them acting as master and node, 1 as node
           - 5 instances, 3 are etcd and nodes, 2 are masters only
           - 7 instances, 3 etcd only, 2 masters, 2 nodes
- test scale up cluster:  +1 etcd, +1 master, +1 node
- godaddy may be able to help with providing compute resources?(stevemcquaid)
- Test dns resolution (kubedns)

### Networking
- romana.io support
- Configure network policy for Calico.
- Opencontrail
- Canal

### High availability
- (to be discussed) option to set a loadbalancer for the apiservers like ucarp/packemaker/keepalived

### Kargo-cli
- option to shutdown services gracefuly and delete instances
- `kargo vagrant` to setup a test cluster locally
- switch to Terraform instead of Ansible for provisionning

### Kargo API
- Perform all actions through an API
- Store inventories / configurations of mulltiple clusters
- make sure that state of cluster is completely saved in no more  than one config file beyond hosts inventory 

### Addons (with kpm)
Include optionals deployments to init the cluster:
##### Monitoring
- Heapster / Grafana ....
- Prometheus  

##### Others
- kubedns
 
##### Dashboards:
 - kubernetes-dashboard
 - Fabric8
 - Tectonic
 - Cockpit

##### Paas like
 - Openshift Origin
 - Openstack
 - Deis Workflow

### Others
- remove nodes  (adding is already supported)
- being able to choose any k8s version (almost done)
- rkt support
- Review documentation (split in categories)
- consul -> if officialy supported by k8s
- Clusters federation option (aka ubernetes)
