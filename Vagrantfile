# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'CentOS_6.5_x86_64'
	config.vm.box_url= 'https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box'
	config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :private_network, ip: '192.168.33.10'

	config.ssh.forward_agent = true

  # ローカルとフォルダ同期
  config.vm.synced_folder 'rails_app', '/home/vagrant/rails_app', create: true, type:'nfs'

  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--memory', 1024]
  end

	config.vm.provision :ansible do |ansible|
		ansible.playbook = 'provision/playbook.yml'
		ansible.inventory_path = 'provision/development'
		ansible.limit = 'all'
	end
end
