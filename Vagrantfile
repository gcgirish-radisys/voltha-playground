# -*- mode: ruby -*-
# # vi: set ft=ruby :

Vagrant.configure(2) do |config|

  (1..3).each do |i|
    config.vm.define "voltha#{i}" do |s|
      s.ssh.forward_agent = true
      s.vm.box = "ubuntu/xenial64"
      #s.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
      s.vm.box_url = "https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box"
      s.vm.hostname = "voltha#{i}"
      s.vm.network "private_network", ip: "172.42.43.10#{i}", netmask: "255.255.255.0",
        auto_config: true,
        virtualbox__intnet: "voltha-net"
      s.vm.provider "virtualbox" do |v|
        v.name = "voltha#{i}"
        v.memory = 2048
        v.gui = false
      end
      s.vm.provision :shell, path: "scripts/bootstrap_host.sh"
    end
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

end
