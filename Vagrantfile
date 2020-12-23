# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "bento/debian-10.6"
    config.vm.network "private_network", ip: "192.168.34.11"
    config.vm.hostname = "vag.mybubbles.me"

    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.manage_guest = true
    config.hostmanager.ignore_private_ip = false

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.pip_install_cmd = "curl https://bootstrap.pypa.io/get-pip.py | sudo python"
    ansible.install_mode = "pip"
    ansible.playbook = "./ansible/hello.yml"
    ansible.version = "latest"
  end
  
  # Optional NFS. Make sure to remove other synced_folder line too
  config.vm.synced_folder './', "/srv/work",
      :nfs => { :mount_options => ["dmode=777","fmode=666"] }
end
