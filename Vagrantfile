# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.box = "nxos/9.3.7"
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end 
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.box_check_update = false
  

    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.raw_arguments = ["-v"]
      ansible.groups = {
        "nxos" => ["nxos-01","nxos-02"],
        "nxos:vars" => {"ansible_connection" => "ansible.netcommon.network_cli",
                          "ansible_network_os" => "cisco.nxos.nxos"
                        }

    }


      config.vm.define "nxos-01" do |node|
        node.vm.boot_timeout = 600
        node.ssh.shell = "run bash"
        node.ssh.insert_key = false
        node.vm.network :private_network, virtualbox__intnet: "link1", auto_config: false
        node.vm.network :private_network, virtualbox__intnet: "link2", auto_config: false
        node.vm.network :private_network, virtualbox__intnet: "link3", auto_config: false 
        node.vm.provider "virtualbox" do |v|
        v.name = "nxos-01"
        v.memory = 8192
        v.customize ["modifyvm", :id, "--uart1", "0x3f8", "4"]
        v.customize ["modifyvm", :id, "--uartmode1", "tcpserver", "2301"]
  
      end
    end
      config.vm.define "nxos-02" do |node|
        node.vm.boot_timeout = 600
        node.ssh.shell = "run bash"
        node.ssh.insert_key = false
        node.vm.network :private_network, virtualbox__intnet: "link1", auto_config: false
        node.vm.network :private_network, virtualbox__intnet: "link2", auto_config: false
        node.vm.network :private_network, virtualbox__intnet: "link3", auto_config: false 
        node.vm.provider "virtualbox" do |v|
        v.name = "nxos-02"
        v.memory = 8192
        v.customize ["modifyvm", :id, "--uart1", "0x3f8", "4"]
        v.customize ["modifyvm", :id, "--uartmode1", "tcpserver", "2302"] 
        if Vagrant.has_plugin?("vagrant-vbguest")
          config.vbguest.auto_update = false
        end
 
        
      end
    end
  end
end