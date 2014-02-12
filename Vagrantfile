Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.ssh.forward_agent = true

  config.vm.network "forwarded_port", guest: 80, host: 8000

  # VirtualBox
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]  
  end


  config.vm.network :private_network, ip: "10.6.6.6"
  config.vm.synced_folder ".", "/vagrant", id: "vagrant-root"

  # This shell provisioner installs librarian-puppet and runs it to install
  # puppet modules. This has to be done before the puppet provisioning so that
  # the modules are available when puppet tries to parse its manifests.
  #
  # Refer to https://github.com/purple52/librarian-puppet-vagrant
  #
  config.vm.provision :shell, :path => "setup.sh"

end
