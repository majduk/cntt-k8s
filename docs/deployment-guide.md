# CNTT Kubernetes Deployment Guide

## High level design description

This Charmed Kubernetes deployment is to be deployed on Openstack with the juju openstack provider. Reder to design document for detailed description of the kubernetes design.

## Preparatory steps

Make sure that the underlaying substrate is configured with:
- flavors 
- tenant with quotas
- images
- security groups
- network
- deployment SSH key

## FCE installation

The [Foundation Cloud Engine](https://launchpad.net/cpe-foundation) is a tool used to drive juju deployment. It should be installed on node that will be used to drive the deployment.

Clone and install the Foundation Cloud Engine:
```
git clone -b stable/2.5 \
  git+ssh://${USERNAME}@git.launchpad.net/cpe-foundation ~/foundation
```
Install Foundation Cloud Engine:
```
cd ~/foundation
sudo ./install
```

## Configure FCE

All `fce` command invocations should be ran from the `./deployment` subdirectory.

Clone this reposiory and go to `./deployment/`. Put openstack credentials unser `keys/`:
```
mkdir keys/
cp openstack.rc keys/
```
Build openstack layer:
```
fce --debug build --layer existing_openstack
```

## Bootsrtap juju
All `fce` command invocations should be ran from the `./deployment` subdirectory.

Juju will first be bootstrapped with a single controller, and then 2 more controllers will be deployed to enable HA for Juju. If the layer is being rebuilt, use `--force` flag.

```
fce --debug build --layer juju_openstack_controller
```
Once this command completes, a juju controller named "k8s-controller" will be created and should work in an HA configuration.

You can verify this by running:
```
juju list-controllers  --refresh
```

## Kubernetes deployment
All `fce` command invocations should be ran from the `./deployment` subdirectory.

Build kubernetes cluster:
```
fce --debug build --layer kubernetes
```

## Validate the cluster

### Juju status

Run `juju status` to make sure that all the units are in active state.

### Kubernetes status

First you need to obtain kubernetes cluster config:
```
mkdir -p ~/.kube
juju scp kubernetes-master/0:config ~/.kube/config
```

After that you can use `kubectl` to interact with the kubernetes cluster.



