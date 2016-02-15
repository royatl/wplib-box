# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "wplib/wplib"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.hostname = "wplib.box"
  config.hostsupdater.aliases = ["underscores.wplib.box", "novarnish.underscores.wplib.box"]
  config.vm.synced_folder "www/underscores", "/srv/sites/underscores.wplib.box", create: true
  config.vm.synced_folder "logs", "/var/log/nginx", create: true
  config.ssh.forward_agent = true
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |vb|
    vb.name = "wplib-box"
  end

  config.vm.provider "vmware" do |vmw|
      vmw.name = "wplib-box"
  end

  config.vm.provision "shell", inline: <<-SHELL
    cd /srv/sites/
    echo "Extracting site files..."
    tar -xzf /srv/sites/underscores.wplib.box.tgz
    sudo service nginx restart
  SHELL

end