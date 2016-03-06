Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_version = "14.04"
  config.vm.hostname = "gnomeontherun-fluentconf"

  # Forwarding for web application
  config.vm.network :forwarded_port, guest: 4200, host: 4200
  # Forwarding for livereload
  config.vm.network :forwarded_port, guest: 49152, host: 49152

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
  end

  config.vm.provision "shell", inline: <<-SHELL

    echo "--------------------------"
    echo "Installing system packages"
    echo "--------------------------"
    # Add NodeJS PPA
    curl -sL https://deb.nodesource.com/setup_5.x | sudo bash -

    sudo apt-get update
    sudo apt-get install -y --force-yes build-essential nodejs git

    echo "-----------------------"
    echo "Installing Node Modules"
    echo "-----------------------"
    npm set progress=false
    sudo npm install --global angular-cli@0.0.23 typings
    cd /vagrant
    npm install
    npm run postinstall -y
    echo "cd /vagrant" >> /home/vagrant/.bashrc
  SHELL
end
