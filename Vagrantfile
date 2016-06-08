# -*- mode: ruby -*-
# vi: set ft=ruby :
box      = 'debian/contrib-jessie64'

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

      node.vm.provision "setup", type: "shell", inline: "DEBIAN_FRONTEND=noninteractive echo 'deb http://ftp.debian.org/debian jessie-backports main contrib non-free' > /etc/apt/sources.list.d/jessie-backports.list && apt-get update && apt-get install -y vim wget htop screen rsync curl git bash-completion apt-transport-https ca-certificates && echo 'deb https://apt.dockerproject.org/repo debian-jessie main' > /etc/apt/sources.list.d/docker.list && apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D && apt-get update && apt-get install -y docker-engine", privileged: true
  end
end
