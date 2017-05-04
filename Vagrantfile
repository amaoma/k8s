# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos7"

  config.vm.define "master" do |kube|
    kube.vm.network :private_network, ip: "192.168.50.50"

    kube.vm.synced_folder ".", "/home/vagrant/k8s", :create => true, :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777,fmode=777']
    kube.vm.synced_folder "../ansible", "/vagrant", :create => true, :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777,fmode=666']

    kube.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--usb", "on"]
    end

    if ARGV[0] == 'up'
      kube.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "k8s_master.yml"
        ansible.limit = "server"
        ansible.inventory_path = 'inventory/localhost'
      end
    end
  end

  config.vm.define "node_lb" do |kube|
    kube.vm.network :private_network, ip: "192.168.50.51"

    kube.vm.synced_folder ".", "/home/vagrant/k8s", :create => true, :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777,fmode=777']
    kube.vm.synced_folder "../ansible", "/vagrant", :create => true, :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777,fmode=666']

    kube.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--usb", "on"]
    end

    if ARGV[0] == 'up'
      kube.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "k8s_lb.yml"
        ansible.limit = "server"
        ansible.inventory_path = 'inventory/localhost'
        ansible.extra_vars = {
          node_ip: '192.168.50.51',
          node_name: 'lb'
        }
      end
    end
  end

  config.vm.define "node_web1" do |kube|
    kube.vm.network :private_network, ip: "192.168.50.52"

    kube.vm.synced_folder ".", "/home/vagrant/k8s", :create => true, :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777,fmode=777']
    kube.vm.synced_folder "../ansible", "/vagrant", :create => true, :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777,fmode=666']

    kube.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--usb", "on"]
    end

    if ARGV[0] == 'up'
      kube.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "k8s_web.yml"
        ansible.limit = "server"
        ansible.inventory_path = 'inventory/localhost'
        ansible.extra_vars = {
          node_ip: '192.168.50.52',
          node_name: 'web1'
        }
      end
    end
  end

  config.vm.define "node_web2" do |kube|
    kube.vm.network :private_network, ip: "192.168.50.53"

    kube.vm.synced_folder ".", "/home/vagrant/k8s", :create => true, :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777,fmode=777']
    kube.vm.synced_folder "../ansible", "/vagrant", :create => true, :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777,fmode=666']

    kube.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--usb", "on"]
    end

    if ARGV[0] == 'up'
      kube.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "k8s_web.yml"
        ansible.limit = "server"
        ansible.inventory_path = 'inventory/localhost'
        ansible.extra_vars = {
          node_ip: '192.168.50.53',
          node_name: 'web2'
        }
      end
    end
  end
end
