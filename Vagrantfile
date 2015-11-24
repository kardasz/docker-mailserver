# -*- mode: ruby -*-
# vi: set ft=ruby :
box      = 'debian/jessie64'

# VM configuration
vm_hostname = 'docker-mailserver'
vm_ram      = '512'
vm_cpus     = 2
vm_pae      = 'on'

Vagrant.configure("2") do |config|
  config.vm.box = box
  config.ssh.forward_agent = true

  config.vm.define 'vm' do |node|
      node.vm.provider "virtualbox" do |v|
          v.customize [
              "modifyvm", :id,
              "--name", vm_hostname,
              "--memory", vm_ram,
              "--cpus", vm_cpus,
              "--pae", vm_pae
          ]
      end

      node.vm.network "private_network", type: "dhcp"
      node.vm.hostname = vm_hostname

      node.vm.provision "update-packages", type: "shell", inline: "/usr/bin/apt-get update; /usr/bin/apt-get upgrade -y; /usr/bin/apt-get autoremove -y", privileged: true
      node.vm.provision "install-packages", type: "shell", inline: "/usr/bin/apt-get -y install vim mc wget htop screen pwgen rsync curl git bash-completion autoconf libtool build-essential", privileged: true
      node.vm.provision "install-docker", type: "shell", inline: "/usr/bin/wget -qO- https://get.docker.com/gpg | /usr/bin/apt-key add - && /usr/bin/wget -qO- https://get.docker.com/ | /bin/sh ", privileged: true
  end
end
