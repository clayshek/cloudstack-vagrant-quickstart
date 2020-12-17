# CloudStack (Nested in Hyper-V) Vagrant Quickstart

Vagrant provisioning of a CloudStack managed KVM virtualization playground / lab, on top of Windows (Hyper-V). For demo purposes.

Still a work in progress, but funcational.

Vagrantfile will provision 3 machines by default, all running CentOS 7:
- csmgmt: CloudStack management server and MySql DB, allocated with 4 GB of vRAM.
- kvm1 & kvm2: QEMU/KVM Hypervisors with CloudStack agent installed, each allocated with 2 GB vRAM. 

Notes:
- Primary goal here is a quick start temporary demo environment. Items like security were not priority. So for example, the MySQL installation is not secured per best practice, and the CloudStack database is created without security in mind, for sake of simplicity. 

## Requirements:

- [Hyper-V: Installed & functional](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v), with a virtual switch that allows outbound Internet connectivity (for package downloads), and DHCP for VM IP addressing.
- [Vagrant installed](https://www.vagrantup.com/downloads)

## Usage:

Clone this repo. Validate appropriateness to your setup of some of the defaults, such as 4 GB RAM to management server VM and 2 GB to each KVM host. 

From within the repo directory, run: `vagrant up`. The only prompts should be asking which Hyper-V virtual switch to use for each VM. The Vagrant Hyper-V provider [can't figure this out yet](https://www.vagrantup.com/docs/providers/hyperv/limitations).

Once Vagrant provisioning is complete, the CloudStack UI should be accessible at 

http://csmgmt.local:8080

Default credentials are `admin / password`, and further setup of CloudStack will be necessary as outlined in the [CloudStack Install Guide](http://docs.cloudstack.apache.org/en/4.14.0.0/installguide/index.html). 

## Cleanup:

Destroy all VMs:  `vagrant destroy --force`  

Destroy specific VMs: `vagrant destroy vmname`

## Reference Docs:

- [CloudStack Quick Install Guide](http://docs.cloudstack.apache.org/en/4.14.0.0/quickinstallationguide/qig.html)
- [CloudStack Install Guide](http://docs.cloudstack.apache.org/en/4.14.0.0/installguide/index.html)
- [How To Build A CloudStack Test Environment](https://www.shapeblue.com/virtualbox-test-env/)


## To-Do

 - [ ] Figure out a better method for assigning static IPs
 - [ ] Setup & configure Primary and Secondary storage
 - [ ] Setup [Primate UI](http://docs.cloudstack.apache.org/en/4.14.0.0/installguide/primate.html#what-is-primate)