# Substrate configuration

## Openstack

### Compute hardware

### Compute
- hugepages
- NUMA
- pinning
- SRIOV
- DPDK
- allocation ratio
- NUMA filter
- sotrage
- virtio 1.1

### Flavors

Flavors for the model are described in [CNTT Reference model 4.2.1.1](https://github.com/cntt-n/CNTT/blob/master/doc/ref_model/chapters/chapter04.md#4211-predefined-compute-flavours):

Basic reference setup only uses:
- cntt-lma: derived from .large
- cntt-k8s-master: derived from .large
- cntt-k8s-worker: derived from .8xlarge

### Infrastructure networking

Networking requirements for the model are described in [CNTT Reference model 4.2.2](https://github.com/cntt-n/CNTT/blob/master/doc/ref_model/chapters/chapter04.md#422-virtual-network-interface-specifications)

### Storage

The reference implementation provides only `.bronze` storage class as defined in [CNTT Reference model 4.2.3](https://github.com/cntt-n/CNTT/blob/master/doc/ref_model/chapters/chapter04.md#423-storage-extensions)