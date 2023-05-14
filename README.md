# openvpn_vagrant_libvirt_ansible

This Vagrant setup creates two VMs to play around with OpenVPN. One is being
configured as the server, one as a client.

Default OS is openSUSE 15.4. Although that can be changed in the Vagrantfile,
please beware that this will break the Ansible provisioning.

## Vagrant

1. You need vagrant obviously. And ansible. And git...
1. Fetch the box, per default this is `opensuse/Leap-15.4.x86_64`, using
   `vagrant box add opensuse/Leap-15.4.x86_64`.
1. Make sure the git submodules are fully working by issuing `git submodule init
   && git submodule update`
1. Run `vagrant up`
1. Connect to the client VM using `vagrant ssh openvpn-client1`. Ping both IPs
   used for OpenVPN (`10.0.0.55` on the client and `10.0.0.1` on the server).
1. Party!

## Disabling the Ansible provisioning

In case you do not want Ansible to install teleport (because you want to install
it yourself), just comment out the following lines in the `Vagrantfile`:

```hcl
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/playbook-all_nodes.yml"
    end # node.vm.provision
```

You also find all of the playbooks in the `ansible` folder.

## License

BSD-3-Clause

## Author Information

I am Johannes Kastl, reachable via kastl@b1-systems.de.
