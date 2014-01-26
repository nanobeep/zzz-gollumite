# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.define ("gollumite") do |gollumite|
    # this gives the VM a better name than 'default'
  end

  # Use nfs for I/O performance gains. See: http://mitchellh.com/comparing-filesystem-performance-in-virtual-machines
  # Enable this if you see issues with I/O speed on the synced folder.
  # It requires `/etc/exports` exist if you're on OSX. If it doesn't, then just `touch /etc/exports`. 
  # You may also be prompted for your password when starting/reloading the VM so that OSX can edit `/etc/exports`.
  # config.vm.synced_folder ".", "/vagrant", type: "nfs"

  # ensure the VM has access to our keys so we can seamlessly use github private repos
  config.ssh.forward_agent = true

  # ip address is fairly arbitrary, if you change it, be sure to update `hosts` file
  config.vm.network :private_network, ip: "192.168.33.10"

  # Note: Also, if you are on a newer version of Virtualbox and you are getting Vagrant warnings about version
  # mismatch for the guest additions, then you should use this plugin: https://github.com/dotless-de/vagrant-vbguest

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. For ease of use, we'll just use the same port.
  config.vm.network :forwarded_port, guest: 4567, host: 4567 # for gollum

  # For information on available options for the Virtualbox provider, please visit:
  # http://docs.vagrantup.com/v2/virtualbox/configuration.html
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

end
