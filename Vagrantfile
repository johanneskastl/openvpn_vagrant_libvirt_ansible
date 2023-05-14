Vagrant.configure("2") do |config|

  # name the VMs
  config.vm.define "openvpn-server" do |node|

    # which image to use
    node.vm.box = "opensuse/Leap-15.4.x86_64"

    # sizing of the VMs
    node.vm.provider "libvirt" do |lv|
      lv.random_hostname = true
      lv.memory = 1024
      lv.cpus = 2
    end

    # set the hostname
    node.vm.hostname = "openvpn-server"

  end # config.vm.define server

  ###############################################

  # define number of clients
  M = 1

  # provision N VMs as clients
  (1..M).each do |i|

    # name the VMs
    config.vm.define "openvpn-client#{i}" do |node|

      # which image to use
      node.vm.box = "opensuse/Leap-15.4.x86_64"

      # sizing of the VMs
      node.vm.provider "libvirt" do |lv|
        lv.random_hostname = true
        lv.memory = 1024
        lv.cpus = 2
      end

      # set the hostname
      node.vm.hostname = "openvpn-client#{i}"

      # if this is the last machine
      if i == M

        #################################################
        # only target one node to not run ansible twice
        # but do not limit this to this node (set ansible.limit to all)
        node.vm.provision "ansible" do |ansible|
          ansible.compatibility_mode = "2.0"
          ansible.limit = "all"
          ansible.groups = {
            "openvpn_clients"  => [ "openvpn-client1" ],
            "openvpn_server"  => [ "openvpn-server" ]
          }
          ansible.playbook = "ansible/playbook-all_nodes.yml"

        end # node.vm.provision

      end # if-condition last machine

    end # config.vm.define clients

  end # each-loop clients

end # Vagrant.configure
