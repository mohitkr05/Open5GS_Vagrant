Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.hostname = "5GCvm"
  config.vm.network "private_network", ip: "192.168.56.101"
  config.vm.synced_folder "data" , "/home/vagrant/data"

  config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = "2048"
     vb.cpus = 2
  end



  # This defines the Open5GS


  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y gnupg wget
    wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
    apt update
    apt install -y mongodb-org mongodb-org-database
    systemctl start mongod
    systemctl enable mongod

    add-apt-repository ppa:open5gs/latest
    apt-get install -y software-properties-common
    apt-get -y update
    apt install -y open5gs
  SHELL
end
