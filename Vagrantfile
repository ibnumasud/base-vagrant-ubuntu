# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.define "base" do |base|

  base.vm.box = "ubuntu/xenial64"
  base.vm.hostname = "base"
  base.vm.synced_folder '.', '/vagrant', disabled: true
  base.vm.network :private_network, ip: "192.168.202.201"
  base.vm.provider "virtualbox" do |vb|
    unless File.exist?('./secondDisk.vdi')
      vb.customize ['createhd', '--filename', './secondDisk.vdi', '--variant', 'Fixed', '--size', 2 * 1024]
    end
    unless File.exist?('./thirdDisk.vdi')
      vb.customize ['createhd', '--filename', './thirdDisk.vdi', '--variant', 'Fixed', '--size', 2 * 1024]
    end
    vb.memory = "1024"
    vb.customize ['storageattach', :id,  '--storagectl', 'SATA', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', './secondDisk.vdi']
    vb.customize ['storageattach', :id,  '--storagectl', 'SATA', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', './thirdDisk.vdi']
  end
  # base.vm.provision :shell, path: "provision.sh", keep_color: "true"
end
end
