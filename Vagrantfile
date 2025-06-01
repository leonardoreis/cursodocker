# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vagrant.plugins = "vagrant-docker-compose"
  config.vm.provision :docker
  config.vm.provision :docker_compose
  config.vm.synced_folder ".", "/home/vagrant/app", type: "virtualbox",
  mount_options: ["dmode=775", "fmode=664"]


  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end

  config.vm.define "ec2" do |vm|
    vm.vm.hostname = "ec2"
    vm.vm.network "forwarded_port", guest: 80, host: 8080
    vm.vm.provision "shell", inline: <<-SHELL
      sudo usermod -aG docker vagrant
    SHELL
  end
end
