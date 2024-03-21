# -*- mode: ruby -*-
# vi: set ft=ruby :
# vi: set tabstop=2 :
# vi: set shiftwidth=2 :

Vagrant.configure("2") do |config|

  vms_debian = [
    { :name => "debian-bullseye",          :box => "generic/debian11",  :vars => {} },
#    { :name => "debian-bookworm",          :box => "generic/debian12",  :vars => {} },
  ]

  config.vm.network "private_network", type: "dhcp"

  vms_debian.each do |opts|
    config.vm.define opts[:name] do |m|

      m.vm.box = opts[:box]

      m.vm.provider "libvirt" do |v|
        v.cpus = 1
        v.memory = 512
      end
      m.vm.provision "ansible" do |ansible|
        ansible.playbook = "tests/test.yml"
        ansible.verbose = 'vv'
        ansible.become = true
        ansible.extra_vars = opts[:vars]
        ansible.raw_arguments = ["-D"]
        ansible.compatibility_mode = "2.0"
      end
    end
  end
end
