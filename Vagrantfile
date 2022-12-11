# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # Use the Debian 11 (Bullseye) base box
    config.vm.box = "debian/bullseye64"
    config.vm.hostname = "grafana-vm"
    config.vm.network "public_network"  
    config.vm.guest = :debian

    config.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = "2048"
      vb.customize ["modifyvm", :id, "--vram", "12"]
    end
    

    config.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update 
      sudo useradd -m -p $(openssl passwd -1 1234) test
      sudo tasksel install xfce-desktop
      sudo apt-get install -y adduser libfontconfig1
      sudo wget https://dl.grafana.com/enterprise/release/grafana-enterprise_9.3.1_amd64.deb
      sudo dpkg -i grafana-enterprise_9.3.1_amd64.deb
      sudo /bin/systemctl daemon-reload
      sudo /bin/systemctl enable grafana-server
      sudo /bin/systemctl start grafana-server
      sudo reboot
    SHELL

  end
  