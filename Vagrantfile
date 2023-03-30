# -*- mode: ruby -*-
# vi: set ft=ruby :

$install_docker_script = <<SCRIPT
echo Installing Docker...
sudo apt-get update
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker vagrant
SCRIPT

BOX_NAME = "ubuntu/focal64"
MEMORY = "1024"
CPUS = 2
MANAGERS = 3
MANAGER_IP = "192.168.57.1"
WORKERS = 3
WORKER_IP = "192.168.57.20"
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    # Common setup
    config.vm.box = BOX_NAME
    config.vm.synced_folder ".", "/vagrant"
    config.vm.provision "shell",inline: $install_docker_script, privileged: true
    config.vm.provider "virtualbox" do |vb|
      vb.memory = MEMORY
      vb.cpus = CPUS
    end
    config.vm.box_check_update = false

    # Setup Manager Nodes
    (1..MANAGERS).each do |i|
        config.vm.define "manager0#{i}" do |manager|
        manager.vm.network :private_network, ip: "#{MANAGER_IP}#{i}"
        manager.vm.hostname = "manager0#{i}"
        if i == 1
            # Example expose port to vagrant host
            # Only configure port to host for Manager01
            manager.vm.network :forwarded_port, guest: 8080, host: 8080
            manager.vm.network :forwarded_port, guest: 9510, host: 9510
        end
        end
    end

    # Setup Woker Nodes
    (1..WORKERS).each do |i|
        config.vm.define "worker0#{i}" do |worker|
            worker.vm.network :private_network, ip: "#{WORKER_IP}#{i}"
            worker.vm.hostname = "worker0#{i}"
        end
    end
end

