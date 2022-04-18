# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"

  config.vm.network "private_network", type: "dhcp"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = "2"
  end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    # Upgrade and install dependancies
    sudo apt update
    sudo apt upgrade -y
    sudo apt install -y gcc make build-essential linux-headers-$(uname -r) virtualbox-guest-additions-iso
    
    # Detect version of go to install based on contents of go.mod
    GO_VERSION=$(grep "go " < /vagrant/go.mod | awk -F' ' '{ print $2 }')
    
    # Install go
    wget https://go.dev/dl/go$GO_VERSION.linux-amd64.tar.gz
    sudo tar -C /usr/local -xzf go$GO_VERSION.linux-amd64.tar.gz
    
    # Set up PATH to go installation
    echo "export PATH=$PATH:/usr/local/go/bin:/home/vagrant/go/bin" >> /home/vagrant/.profile

    # Install gosec and staticcheck
    source /home/vagrant/.profile
    go install github.com/securego/gosec/v2/cmd/gosec@latest
    go install honnef.co/go/tools/cmd/staticcheck@latest
    
    # Install project dependancies
    cd /vagrant && go mod download

    # Print out ip address for vm
    ip addr | grep -v "inet6" | grep -v "127.0.0.1" | grep "inet"

    # Happy hacking
    echo "lambdajack wishes you happy hacking!"
  SHELL
end
