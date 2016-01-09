# Magento 2 Virtual boxes setup
This repository contains YAML files that define minimal VM setup for load balancer followed by Magento 2 installation. 

Note: Contents of this repository are intended to be used with 
[multi box vagrant with puppet setup we provide](https://github.com/the-shop/Vagrant) only.

## Flow
Vagrant iterates over all files that match following `*.yaml` and presumes they are the definitions of VMs.

YAML files are prepended with integers so that they boot and provision in correct order (i.e. magento2 box needs mysql 
box to be available, and that's on `database` box).

## Tweaking resources
This pre-defined setup is intended for development machines with quad core CPUs and at least 8 GB of RAM. If you have 
more than that, feel free to bump up numbers defined in `puphpet/boxes/*.yaml` files (`memory` and `cpus` fields)

## Adding boxes
Adding boxes is as simple as adding a new YAML file to root directory. Make sure there are no collisions in 
names, hostnames, VM names and IPs and you should be good to go.

If you wish to add Magento 2 box to load balancer rotation, you'll need to modify 
`hiera/loadbalancer_data.yaml`. If you wish to add load balancing in front of anything else, you'll need to 
create new load balancer box with own setup.

When adding load balancers, it's important that it matches `/^*loadbalancer$/` regex.

## IMPORTANT
**For now, this is intended for local setup only, there might be security implications if used on production 
so please DO NOT USE THIS ON PRODUCTION.**