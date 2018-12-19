# -*- mode: ruby -*- 
# vi: set ft=ruby : 
# Every Vagrant development environment requires a box. You can search for 
# boxes at https://atlas.hashicorp.com/search. 
BOX_IMAGE = ""centos/7"" 
NODE_COUNT = 2

Vagrant.configure("2") do |config|
   config.vm.define "master" do |subconfig|
     subconfig.vm.box = BOX_IMAGE
     subconfig.vm.hostname = "master"
     subconfig.vm.network :private_network, ip: "10.0.0.10"
	 
	 subconfig.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--name", "web"]
	 end
   end
   
   (1..NODE_COUNT).each do |i|
    config.vm.define "srv01cen#{i}" do |subconfig|
	 subconfig.vm.box = BOX_IMAGE
	 subconfig.vm.hostname = "srv01cen#{i}"
	 subconfig.vm.network :private_network, ip: "10.0.0.#{i + 10}"
	 
	 subconfig.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--name", "db"]
	 end
    end
  end   
   # Install avahi on all machines
   config.vm.provision "shell", inline: <<-SHELL
   yum clean all
   yum update -y
   SHELL
end
