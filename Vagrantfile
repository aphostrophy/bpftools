# -*- mode: ruby -*-
# vi: set ft=ruby :
ENV['VAGRANT_DEFAULT_PROVIDER'] = "virtualbox"

VAGRANTFILE_API_VERSION = "2"

$bootstrap=<<SCRIPT
sudo apt-get clean
sudo apt update -y
sudo apt install build-essential git make libelf-dev clang strace tar bpfcc-tools linux-headers-$(uname -r) gcc-multilib -y
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	ipv4 = "192.168.33.10"
	config.vm.define "bpfbook" do |ubuntu|
        ubuntu.vm.box = "generic/ubuntu2004"
		# fedora.vm.box_version = "30.20190425.0"
		net_index = 1
		ubuntu.vm.hostname = "bpfbook"
		ubuntu.vm.provider "virtualbox" do |vb|
            vb.name = "bpf_dev_ubuntu"
			vb.customize ["modifyvm", :id, "--memory", "1024"]
		end
		ubuntu.vm.provider "libvirt" do |lv|
			lv.memory = 1024
		end
		ubuntu.vm.network :private_network, ip: "#{ipv4}"
		ubuntu.vm.provision :shell, inline: $bootstrap, :args => "#{ipv4}"
	end
end