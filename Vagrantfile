# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  #Base box OS
  config.vm.box = "elastic/ubuntu-16.04-x86_64"
  #Disable box update check
  config.vm.box_check_update = false
  #Configure virtualbox virtual machine
  config.vm.provider "virtualbox" do |vb|
		#virtual machine name
		vb.name = "FirstVM"
		#virtual machine memory
		vb.memory = "4096"
		#virtual machine CPUs
		vb.cpus= "4"
	end
	
	#Configure forwarded ports
	config.vm.network "forwarded_port", guest: 9200, host: 9200, auto_correct: true
	config.vm.network "forwarded_port", guest: 9300, host: 9300, auto_correct: true
	config.vm.network "forwarded_port", guest: 5601, host: 5601, auto_correct: true
	#Installation et lancement de Ansible
	provisioner = Vagrant::Util::Platform.windows? ? :ansible_local : :ansible
	config.vm.provision provisioner do |ansible|
		ansible.playbook = "FirstVM.yml"
		ansible.install_mode = :pip
		ansible.version = "latest"
		ansible.limit = "all"
	end
end
