# Magento 2 Virtual boxes setup
This repository contains YAML files that define minimal VM setup for distributed Magento 2project. 

Note: Contents of this repository are intended to be used with 
[multi box vagrant with puppet setup we provide](https://github.com/the-shop/Environments) only.

## Setup
  - Before you run the `up` command, copy file `puphpet/boxes/Magento2/hiera/magento2_data.yaml.dist` to 
 `puphpet/boxes/Magento2/hiera/magento2_data.yaml` and update contents of copied file. Magento connect data is 
 mandatory in order to get `magento2-01` box up and running. Instructions are available here: 
  ([magento connect credentials](https://www.magentocommerce.com/magento-connect/customerdata/secureKeys/list/))
  - Hosts setup: append `192.168.56.120 magento2distributed.dev` line to your 
  [hosts file](https://en.wikipedia.org/wiki/Hosts_(file)#Location_in_the_file_system). Database can be accessed at 
  `192.168.56.121`, and direct access to Magento 2 box is on `192.168.56.122`
  - Load Balancer statistics can be accessed at `http://magento2distributed.dev/haproxy?stats` with username `haproxy` 
  and password `password` - credentials can be changed in `puphpet/boxes/Magento2/hiera/loadbalancer.yaml` file.
  - Distributed Magento 2 will be accessible through load balancer at 
  [http://magento2distributed.dev](http://magento2distributed.dev).

## Tweaking resources
This pre-defined setup is intended for development machines with quad core CPUs and at least 8 GB of RAM. If you have 
more than that, feel free to bump up numbers defined in `puphpet/boxes/*.yaml` files (`memory` and `cpus` fields)

## Adding boxes
Adding boxes is as simple as adding a new YAML file to root directory. Make sure there are no collisions in 
names, hostnames, VM names and IPs and you should be good to go.

If you wish to add STAR Commerce frontend box to load balancer rotation, you'll need to modify 
`puphpet/boxes/Magento2/hiera/loadbalancer_data.yaml`. If you wish to add load balancing in front of anything else, 
you'll need to create new load balancer box with own setup.

When adding load balancers, it's important that hostname matches `/^*loadbalancer$/` regex.

## IMPORTANT
**For now, this is intended for local setup only, there might be security implications if used on production 
so please DO NOT USE THIS ON PRODUCTION.**