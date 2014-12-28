VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  ## see https://vagrantcloud.com/ubuntu/boxes/trusty64
  ## it should be downloading from https://atlas.hashicorp.com/ubuntu/boxes/trusty64/versions/14.04/providers/virtualbox.box
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "192.168.33.77"
  config.vm.hostname = "cakephpdev"

  #Add any alias:
  config.hostsupdater.aliases = [
    "cake3.dev"
  ]

  # feel free to change
  config.vm.synced_folder ".", "/vagrant", :nfs => true

  # Fix for Ansible bug resulting in an encoding error
  ENV['PYTHONIOENCODING'] = "utf-8"

  config.vm.provision "ansible" do |ansible|
    ansible.limit = 'all'
    ansible.playbook = "ansible/development.yml"
    ansible.inventory_path = "ansible/hosts"
  end

  config.vm.post_up_message = "\n\nProvisioning is done, visit http://app.dev for your CakePHP application! \n\nVisit http://phpmyadmin.app.dev for phpMyAdmin (MySQl credentials are root:temppassword).\n\n"
end
