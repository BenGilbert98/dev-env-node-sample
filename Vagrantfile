# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.network "private_network", ip: "192.168.10.100"
  # config.hostsupdater.aliases = ["development.local"]

  # Sync the app folder(not copying in. Its syncing)
  #
  config.vm.synced_folder "app", "/app"

  # run the provision script
  config.vm.provision "shell", path: "environment/provision.sh"
end