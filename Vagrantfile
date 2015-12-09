# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = 'ubuntu/trusty64'
  config.vm.hostname = 'ruby.dev'
  config.vm.network "private_network", ip: "192.168.50.99"
  config.vm.network "public_network"
  config.vm.provider :virtualbox do |vb|
    vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", "4096"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end



  $script = <<SCRIPT

apt-get update -y
apt-get upgrade -y
apt-add-repository -y ppa:brightbox/ruby-ng
apt-get install -y ruby2.2 ruby 2.2-dev
apt-get install -y ntp
apt-get install -y build-essential
apt-get install -y g++
apt-get install -y make libqt4-dev libpq-dev cmake
apt-get install -y curl libcurl3 libcurl4-gnutls-dev
apt-get install -y zlib1g-dev unzip wget
apt-get install -y openjdk-7-jre 
apt-get install -y openjdk-7-jdk
apt-get install -y imagemagick libmagickwand-dev
apt-get install -y libmysqlclient-dev libmysqld-dev
apt-get install -y libssh2-php
apt-get install -y libicu-dev
apt-get install -y libkrb5-dev
apt-get install -y bison
apt-get install -y mcrypt
apt-get install -y libssl-dev libyaml-dev libreadline-dev openssl zlib1g-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev
apt-get install -y libsqlite3-dev sqlite3
apt-get install -y ruby1.9.1-dev
apt-get install -y python-software-properties
apt-get install -y redis-server
apt-get install -y git-core
apt-get install -y nodejs
apt-get install -y memcached
apt-get install -y monit
apt-get install -y apache2
apt-get install -y apache2-threaded-dev libapr1-dev libaprutil1-dev


# Java Environment
/usr/sbin/update-locale LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8
export JAVA_HOME="/usr/lib/jvm/java-7-openjdk-amd64"
echo JAVA_HOME="/usr/lib/jvm/java-7-openjdk-amd64" >> /etc/environment


# Testing Services
add-apt-repository ppa:ubuntu-mozilla-security/ppa
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sh -c 'echo deb https://dl.google.com/linux/chrome/deb/ stable main > /etc/apt/sources.list.d/google.list'
apt-get update -y
apt-get install -y xfonts-100dpi xfonts-75dpi xfonts-scalable xfonts-cyrillic xvfb x11-apps  imagemagick firefox google-chrome-stable
apt-get install -y qt5-default libqt5webkit5-dev
apt-get install -y libqtwebkit-dev
mkdir -p /var/lib/chrome-driver
mkdir -p /var/lib/selenium
cp /vagrant/drivers/selenium*.jar /var/lib/selenium/selenium-server.jar
cp /vagrant/drivers/chromedriver /var/lib/chrome-driver/chromedriver
export DISPLAY=:99
echo "DISPLAY=:99" >> /etc/environment


cd /vagrant
bundle install
rake db:create && rake db:setup
bundle exec rspec





SCRIPT



  config.vm.provision "shell", inline: $script

    end
