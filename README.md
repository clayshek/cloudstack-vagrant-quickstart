# CloudStack (Nested in Hyper-V) Vagrant Quickstart

Vagrant provisioning of a CloudStack managed KVM virtualization playground, on top of Windows (Hyper-V). For demo purposes.

Still very much a work in progress, and currently only partially funcational.

Vagrantfile will provision 3 machines by default:
- csmgmt: CloudStack management server and MySql DB. CentOS 7.
- kvm1 & kvm2: QEMU/KVM Hypervisors with CloudStack agent installed. CentOS 7

## Requirements:

- [Hyper-V: Installed & functional](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v), with a virtual switch that allows outbound Internet connectivity (for package downloads)
- [Vagrant installed](https://www.vagrantup.com/downloads)

## Usage:

Clone this repo. From within the repo directory, run: `vagrant up`. The only prompt should be asking which Hyper-V virtual switch to use. The Vagrant Hyper-V provider [can't figure this out yet](https://www.vagrantup.com/docs/providers/hyperv/limitations).

## Cleanup:

Destroy all VMs:  `vagrant destroy --force`  

Destroy specific VMs: `vagrant destroy vmname`

## Reference Docs:

- [CloudStack Quick Install Guide](http://docs.cloudstack.apache.org/en/4.14.0.0/quickinstallationguide/qig.html)
- [CloudStack Install Guide](http://docs.cloudstack.apache.org/en/4.14.0.0/installguide/index.html)
- [How To Build A CloudStack Test Environment](https://www.shapeblue.com/virtualbox-test-env/)
