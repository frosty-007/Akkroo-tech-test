# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
BASE_HOSTNAME = "AKKROO-WEB-0"
BASE_IP = "10.0.1.1"
NUM_MACHINES = 3
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  (0..NUM_MACHINES-1).each do |id|

    config.vm.define "AKKROO-WEB-0#{id}" do |machine|
	machine.vm.box = "centos/7"
	machine.vm.hostname = "#{BASE_HOSTNAME}#{id}"
	machine.vm.network "private_network", ip: "#{BASE_IP}#{2+id}"
 	machine.vm.network "forwarded_port", guest: "80", host: "800#{id}"
	machine.vm.provider :virutalbox do |v|
		v.customize ["modifyvm", :id, "--name", "#{BASE_HOSTNAME}#{id}"]
		v.customize ["modifyvm", :id, "--memory", 512]
		v.customize ["modifyvm", :id, "--cpus", 1]
end
# Provisioning configuration for Ansible.
   config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
      ansible.verbose = "v"
	end
	
	machine.ssh.insert_key = false
	if id == NUM_MACHINES
	
    end
   end
 end
end

