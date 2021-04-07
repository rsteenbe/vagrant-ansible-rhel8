# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.define "server1" do |server1|
    server1.vm.box = "generic/rhel8"
	
	server1.vm.network 'forwarded_port', guest: 2222, host: 2222
	server1.vm.network 'forwarded_port', guest: 29200, host: 29200
  
	server1.vm.network 'forwarded_port', guest: 5005, host: 5005
	server1.vm.network 'forwarded_port', guest: 8787, host: 8787
	server1.vm.network "private_network", ip: "192.168.50.10"
	server1.vm.provider "virtualbox" do |v|
		v.memory = 4096
		v.cpus = 2
	end
	server1.vm.provision "shell", inline: <<-SHELL
    /bin/echo "================= Client Server 1 Running ================"

	SHELL
	#config.ssh.username = "vagrant"
	#config.ssh.password = "vagrant"
	#config.ssh.insert_key = false
  end
  
  config.vm.define "server2" do |server2|
    server2.vm.box = "generic/rhel8"
	
	server2.vm.network 'forwarded_port', guest: 8181, host: 8181
	server2.vm.network 'forwarded_port', guest: 29201, host: 29201
  
	server2.vm.network 'forwarded_port', guest: 5006, host: 5006
	server2.vm.network 'forwarded_port', guest: 8788, host: 8788
	server2.vm.network "private_network", ip: "192.168.50.12"
	server2.vm.provider "virtualbox" do |v|
		v.memory = 4096
		v.cpus = 2
	end
	server2.vm.provision "shell", inline: <<-SHELL
    /bin/echo "================= Client Server 2 Running ================"

	SHELL
	#config.ssh.username = "vagrant"
	#config.ssh.password = "vagrant"
	#config.ssh.insert_key = false
  end
  
  config.vm.provision "shell", inline: "echo Provision 2 ubuntu/xenial64 boxes"
	
    config.vm.define "ansible" do |ansible|
    ansible.vm.box = "bento/ubuntu-20.04"
	ansible.vm.network 'forwarded_port', guest: 9200, host: 9200
	ansible.vm.network 'forwarded_port', guest: 9300, host: 9300
	ansible.vm.network "private_network", ip: "192.168.50.11"
	ansible.vm.provider "virtualbox" do |v|
		v.memory = 2048
		v.cpus = 2
	end
	ansible.vm.provision "shell", inline: <<-SHELL
	/bin/echo "================= Installation Ansible Started ================"
	sudo apt update
	sudo apt install software-properties-common -y
	sudo apt-add-repository --yes --update ppa:ansible/ansible
	sudo apt install ansible -y
	sudo apt install sshpass -y
	# ssh-keyscan -H 192.168.50.10 >> ~/.ssh/known_hosts
	sed -i 's/#host_key_checking = False/host_key_checking = False/' /etc/ansible/ansible.cfg
	/bin/echo "================= Installation Ansible Finished ================"
	/bin/echo "Commands to SSH:"
	/bin/echo "vagrant ssh ansible"
	/bin/echo "vagrant ssh server1"
	/bin/echo ""
	/bin/echo "IP Asible: 192.168.50.11"
	/bin/echo "IP Server1: 192.168.50.10"
	/bin/echo "IP Server2: 192.168.50.12"
	SHELL
  end
  
  
end