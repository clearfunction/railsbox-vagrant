# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  # mailcatcher
  config.vm.network "forwarded_port", guest: 1025, host: 1025
  config.vm.network "forwarded_port", guest: 1080, host: 1080

  config.vm.network "forwarded_port", guest: 3000, host: 3000

  config.ssh.forward_agent = true
  config.ssh.shell = "/bin/bash -l"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     #vb.gui = true
  
     # Customize the amount of memory on the VM:
     vb.memory = "4096"
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update

     sudo apt-get -f install

     # databases
     sudo apt-get install -y redis-server fish
     sudo add-apt-repository "deb https://apt.postgresql.org/pub/repos/apt trusty-pgdg main"
     wget --quiet -O - https://postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - 
     sudo apt-get update
     sudo apt-get install postgresql-9.4


	# easy rails db logins
     sudo -u postgres createuser -s -w vagrant

     # node is good
     curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
     sudo apt-get install -y nodejssudo apt-get install nodejs
     sudo apt-get install -y nodejs npm
     sudo npm install -g yarn

     # shell convenience
     sudo apt-get install -y tmux tree silversearcher-ag htop aptitude

     # dev lib stuff
     sudo apt-get install -y vim curl wget
     sudo apt-get install -y git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev libgmp3-dev

     # dev headers
     sudo apt-get install -y libmagickwand-dev # rmagick, imagemagick
     sudo apt-get install -y libpq-dev postgresql-client-common     # postgres
     #sudo apt-get install -y libmysqlclient-dev mysql-client
     sudo apt-get install -y libgsl0-dev  # sciencey text for jekyll

     git config --global alias.co checkout
     git config --global alias.st status
     git config --global alias.br branch
   SHELL
end
