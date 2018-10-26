# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

    config.vm.box = "marcosrmendez/github-pages"

    config.vm.box_check_update = true

    config.vm.network "forwarded_port", guest: 4000, host: 4000

    #config.vm.network "private_network", ip: "192.168.33.10"

    config.vm.network "public_network"

    #share the ssh keys from your host box
    config.vm.synced_folder "~/.ssh", "/home/vagrant/.ssh", SharedFoldersEnableSymlinksCreate: false

    config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", 512]
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end

    #set the git user and email from your host box
    if File.exists?(File.join(Dir.home, ".gitconfig"))

      git_name = `git config user.name`   # find locally set git name
      git_email = `git config user.email` # find locally set git email

      # set git name for 'vagrant' user on VM
      config.vm.provision :shell, privileged: true, :inline => "git config --global user.name '#{git_name.chomp}'"
      # set git email for 'vagrant' user on VM
      config.vm.provision :shell, privileged: true, :inline => "git config --global user.email '#{git_email.chomp}'"

    end

    config.vm.provision "shell", privileged: false, path: "script/vagrant"
    #config.vm.provision "shell", privileged: false, path: "script/server", run: "always"

end
