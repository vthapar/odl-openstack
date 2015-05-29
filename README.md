# odl-openstack
This repository contains different local.conf scripts which can be used to create a devstack based setup with Opendaylight and Openstack.

./master: This folder contains local.conf scripts to be used with master branch of devstack
./juno: This folder contains local.conf scripts to be used with stable/juno branch of devstack
./kilo: This folder contains local.conf scripts to be used with stable/kilo branch of devstack

# Pre-requisites
----------------
These depend mainly on type of setup.

allinone: This refers to single node devstack and ODL running on same node. Recommended minimum for this setup is VM with GB RAM and at least 4 cores.

singlenode: This refers to single node devstack setup with ODL running on an external node. This external node could be another VM or host.

multinode: This refers to multinode devstack setup with ODL running on external node. The compute local.conf files in this one can be used to add additional compute nodes to an existing allinone or singlenode setup also. Requirements for controller node are same as allinone/singlenode with an extra VM/Host per compute node.


# Configuration
---------------
These are some of the key changes to be made in local.conf

HOST_IP: This should be the IP of where where you're running devstack.
HOST_NAME: Same as above but hostname instead of IP Address.

OFFLINE: First time you run devstack this needs to be False. For subsequent runs you can make it True.

SERVICE_HOST_NAME: For multi-node setups this should be IP of where you're running OpenStack controller.
SERVICE_HOST: Same as above but IP Address instead of hostname.

NEUTRON_CREATE_INITIAL_NETWORKS: Devstack creates two networks by default. Set it to false if you don't want to create your own networks. Note that if this is set to true and there are some connectivity issues between devstack and ODL, devstack will fail and you will have to restart.

ODL_MODE [kilo+ only]: Can be externalodl, allinone or compute. Terms are self-explanatory.
ODL_MGR_IP: This is the IP Address of node where ODL is running.
ODL_LOCAL_IP: This is needed if you want to use a separate data interface to carry vxlan/gre tunnel traffic.
ODL_PROVIDER_MAPPINGS: If you were using OVS_PROVIDER_MAPPINGS in your non-odl setup, this is where you should specify your provider mappings.

For more details refer: https://github.com/stackforge/networking-odl/blob/master/devstack/settings

# HowTo run
-----------
1. Clone the devstack repo and set branch to juno/kilo/master
2. Run ODL and once you get karaf console run 'feature:install odl-ovsdb-openstack'. Add any additional features you may require ['odl-dlux-core' etc]
3. Once ODL is up and running, copy the appropriate local.conf.x file to your devstack directory and rename it to local.conf
4. Run './stack/sh'
5. If all goes fine you should get the success message and URL to open Horizon UI.


# Useful links
--------------
These are the links which provided most of the information you see here:

1. [Ask OpenDaylight] (https://ask.opendaylight.org/questions/)
2. [ODL+Openstack wiki] (https://wiki.opendaylight.org/view/OpenStack_and_OpenDaylight)
3. [Devstack github] (https://github.com/openstack-dev/devstack)
4. [Stackforge for ODL Plugin] (https://github.com/stackforge/networking-odl)
5. [Flavio's mail on running networking-odl plugin with ODL] (https://lists.opendaylight.org/pipermail/ovsdb-dev/2015-February/001132.html)
6. [Mohnish's mail on enabling Neutron Router API with devstack and ODL] (https://lists.opendaylight.org/pipermail/ovsdb-dev/2015-April/001400.html)
7. [Romil's scripts to install ODL+OpenStack from canonical packages] (https://github.com/romilgupta/Openstack-ODL-Script)

8. [Slides from the workshop conducted at ODL India Forum 2015]
(http://events.linuxfoundation.org/sites/events/files/slides/ODL%20and%20OpenStack%20-%20Workshop.pdf)

9. [Flavio's Blog part1 (link to part2 at end of blog)] http://www.flaviof.com/blog/work/how-to-odl-with-openstack-part1.html
