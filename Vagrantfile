# -*- mode: ruby -*-
# vi: set ft=ruby :

libsass_version = ENV.fetch('LIBSASS_VERSION', '3.3.2')
sassc_version = ENV.fetch('SASSC_VERSION', '3.3.0')

Vagrant.configure(2) do |config|
  config.vm.box = "puphpet/ubuntu1404-x64"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y automake libtool git build-essential
    git clone https://github.com/sass/libsass.git
    git clone https://github.com/sass/sassc.git libsass/sassc
    cd libsass && git checkout '#{libsass_version}' && autoreconf --force --install && make -j5 && cd ..
    cd libsass/sassc && git checkout #{sassc_version} && SASS_LIBSASS_PATH=../ make && cd ../..
    cp libsass/sassc/bin/sassc /vagrant/support
  SHELL
end
