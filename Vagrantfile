# set up the default terminal
ENV["TERM"]="linux"

Vagrant.configure("2") do |config|

  # set up root access
  config.ssh.username = 'root'
  config.ssh.password = 'vagrant'
  config.ssh.insert_key = 'true'

  NodeCount = 1

  # configure Kubernetes Nodes
  (1..NodeCount).each do |i|
    config.vm.define "node#{i}" do |node|
      # set base image for the vagrant box
      # Use any version shown here https://app.vagrantup.com/opensuse/boxes/Leap-15.4.x86_64
      config.vm.box = "opensuse/Leap-15.4.x86_64"
      config.vm.box_version = "15.4.13.7"
      
      # Run ifconfig or ip a to find the appropriate interface
      config.vm.network "public_network", :adapter=>3, bridge: "br1"
      
      # NOTE: This will enable public access to the opened port
      config.vm.network "forwarded_port", guest: 8080, host: 8080
      config.vm.network "forwarded_port", guest: 9090, host: 9090
      config.vm.network "forwarded_port", guest: 9100, host: 9100
      config.vm.network "forwarded_port", guest: 9376, host: 9376
      config.vm.network "forwarded_port", guest: 3000, host: 3000

      # set the static IP for the vagrant box
      node.vm.network "private_network", ip: "192.168.50.10#{i}"
      # configure the parameters for VirtualBox provider
      node.vm.provider "virtualbox" do |v|
        v.name = "node#{i}"
        v.memory = 8192
        v.cpus = 2
      end
    # Bootstrap the machine
    config.vm.provision "shell", path: "bootstrap.sh"
    end
  end
end