# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
  sudo apt-get update
  sudo apt-get install -y build-essential
  sudo apt-get install -y curl
  
  gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3  
  curl -sSL https://get.rvm.io | bash -s stable --ruby
  source /usr/local/rvm/scripts/rvm
  
  curl -sL https://deb.nodesource.com/setup | sudo bash -
  sudo apt-get install -y nodejs
  
  rvm use default
  gem install jekyll  
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/precise32"
  config.vm.network "forwarded_port", guest: 4000, host: 4000
  config.vm.provision "shell", inline: $script
end
