# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.disksize.size = '50GB'

  config.vm.provider "virtualbox" do |v|
    v.name = "rainbond"
  end

  config.vm.box_check_update = false
  #config.vm.synced_folder ".", "/opt"

  config.vm.provider "virtualbox" do |vb|
  # Display the VirtualBox GUI when booting the machine
    vb.gui = false
    vb.memory = "4096"
  end

  config.vm.network "private_network", ip: "192.168.21.21"

  config.vm.provision "shell", inline: <<-SHELL
    wget https://pkg.rainbond.com/releases/common/v5.0/grctl
    chmod +x grctl
    systemctl disable systemd-resolved.service
    systemctl stop systemd-resolved
    echo "nameserver 114.114.114.114" > /etc/resolv.conf

    apt update && apt-get install -y docker.io 
    usermod -aG docker vagrant
    #cp /vagrant/.bashrc /home/vagrant/.b
    cp grctl /opt
    cd /opt
    ./grctl init --iip 192.168.21.21 --eip 192.168.21.21

  SHELL
end

