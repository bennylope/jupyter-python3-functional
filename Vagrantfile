# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 8888, host: 8888, auto_correct: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo add-apt-repository ppa:fkrull/deadsnakes -y
    sudo apt-get update
    sudo apt-get install -y python3.5 python3.5-dev python3-pip python3-dev
    # sudo mv /usr/bin/python3 /usr/bin/python3-old
    # sudo ln -sfn /usr/bin/python3.5 /usr/bin/python3
    wget https://bootstrap.pypa.io/get-pip.py
    sudo python3 get-pip.py
    sudo pip3 install setuptools --upgrade
    sudo pip3 install --upgrade ipython[all] jupyter[all] jupyter_core jinja2
    sudo mkdir -p /vagrant/notebook
  SHELL

  config.vm.provision "shell", run: "always", inline: <<-SHELL
    sudo pip install -r /vagrant/requirements.txt
    sudo python3 /vagrant/RISE/setup.py install
    killall ipython3
    sleep 3
    ipython3 notebook --notebook-dir=/vagrant/notebook --no-browser --ip=0.0.0.0 &
  SHELL

end
