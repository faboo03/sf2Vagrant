Vagrant.configure("1") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "saucy-server-cloudimg-amd64-vagrant-disk1.box"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/saucy/20131019/saucy-server-cloudimg-amd64-vagrant-disk1.box"

  # Boot with a GUI so you can see the screen. (Default is headless)
  config.vm.boot_mode = :gui

  # Assign this VM to a host only network IP, allowing you to access it
  # via the IP.


  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  # deprecated in 0.9.0
  #config.vm.forward_port "http", 80, 8080
  config.vm.forward_port 80, 8080  
  
  #deprecated in 0.9.0
  #config.vm.network "33.33.33.10"
  config.vm.network :hostonly, "33.33.33.10"

  if !RUBY_PLATFORM.include? "mswin"
    config.vm.share_folder("vagrant-root", "/vagrant", ".", :mount_options => "dmode=777,fmode=777", :nfs => true)
  end

  # increase default memory capacity
#  config.vm.customize ["modifyvm", :id, "--memory", "1024"]
	
  # Enable provisioning with chef solo, specifying a cookbooks path (relative
  # to this Vagrantfile), and adding some recipes and/or roles.
  #
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
#    chef.add_recipe "symfony2"
	
	chef.add_recipe("apt")
	chef.add_recipe("build-essential")
	chef.add_recipe("xml")
	chef.add_recipe("mysql")
	chef.add_recipe("apache2::mod_php5")
	chef.add_recipe("apache2::mod_rewrite")
	chef.add_recipe("php::module_apc")
	chef.add_recipe("php::module_mysql")
	chef.add_recipe("php-modules")
	chef.add_recipe("git")
	chef.add_recipe("composer")
	chef.add_recipe("hostfile")
		
    # You may also specify custom JSON attributes:
    chef.json.merge!({
      'mysql' => {
        :server_root_password => "geoRaci9"
      },
      "php" => {
        "conf_dir" => '/etc/php5/apache2',
        "directives" => {
            'date.timezone' => 'Europe/London',
            'short_open_tag' => 0,
        }
      }
    })
  end

  # Enable provisioning with chef server, specifying the chef server URL,
  # and the path to the validation key (relative to this Vagrantfile).
  #
  # The Opscode Platform uses HTTPS. Substitute your organization for
  # ORGNAME in the URL and validation key.
  #
  # If you have your own Chef Server, use the appropriate URL, which may be
  # HTTP instead of HTTPS depending on your configuration. Also change the
  # validation key to validation.pem.
  #
  # config.vm.provision :chef_client do |chef|
  #   chef.chef_server_url = "https://api.opscode.com/organizations/ORGNAME"
  #   chef.validation_key_path = "ORGNAME-validator.pem"
  # end
  #
  # If you're using the Opscode platform, your validator client is
  # ORGNAME-validator, replacing ORGNAME with your organization name.
  #
  # IF you have your own Chef Server, the default validation client name is
  # chef-validator, unless you changed the configuration.
  #
  #   chef.validation_client_name = "ORGNAME-validator"
end