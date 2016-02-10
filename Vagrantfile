# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "puppetlabs/ubuntu-14.04-64-puppet"

  #config.vm.synced_folder "OpenWRT_build", "/tmp/OpenWRT_build"


  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
     sudo apt-get install -y apache2
     sudo apt-get install -y unzip
     sudo apt-get install -y libssl-dev
   SHELL

  config.vm.provider :virtualbox do |vb|

    vb.customize ["modifyvm", :id, "--memory", 1024]
    vb.customize ["modifyvm", :id, "--cpus", 2]

  end

  config.vm.provision :chef_solo do |chef|

    chef.cookbooks_path = "./cookbooks"
    chef.add_recipe "OpenWRT"

    chef.json = {
      :OpenWRT => {
        # -- Sample Overrides --
        # :ssh_key => 'id_rsa',
        # :firmware_platform => 'brcm47xx',
        # :firmware_image_builder => 'brcm47xx',
        # :firmware_profile => 'WRTSL54GS',
        # :firmware_model => 'wrtsl54gs',
        # :firmware_file => 'openwrt-wrtsl54gs-squashfs.bin'
      }
    }

  end

end
