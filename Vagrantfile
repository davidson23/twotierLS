# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  

  config.vm.provider "virtualbox" do |v|
    v.gui=false

  end
  
  ##### DEFINE VM for Spine1 #####
  config.vm.define "Spine1" do |device|
    
    device.vm.hostname = "Spine1" 
    
    device.vm.box = "CumulusCommunity/cumulus-vx"
    device.vm.provider "virtualbox" do |v|
      v.name = "Spine1"
      v.customize ["modifyvm", :id, '--audiocontroller', 'AC97', '--audio', 'Null']
      v.memory = 1024
    end
    
    device.vm.synced_folder ".", "/vagrant", disabled: true
	
    # NETWORK INTERFACES
      # link for swp1 --> to_Leaf1
      device.vm.network "private_network", virtualbox__intnet: "sw_L1SP1", auto_config: false , :mac => "a00000000021"
      # link for swp2 --> to_Leaf2
      device.vm.network "private_network", virtualbox__intnet: "sw_L2SP1", auto_config: false , :mac => "44383900005c"
      # link for swp3 --> to_Leaf3
      device.vm.network "private_network", virtualbox__intnet: "sw_L3SP1", auto_config: false , :mac => "44383900002f"
      # link for swp4 --> to_Leaf4
      device.vm.network "private_network", virtualbox__intnet: "sw_L4SP1", auto_config: false , :mac => "443839000058"
	  
    device.vm.provider "virtualbox" do |vbox|
      vbox.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', "--nictype2", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all', "--nictype3", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc4', 'allow-all', "--nictype4", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc5', 'allow-all', "--nictype5", "virtio"]
      vbox.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end

    # Run Any Extra Config
    device.vm.provision :shell , path: "./helper_scripts/config_Spine1.sh"
	
end

  ##### DEFINE VM for Spine2 #####
  config.vm.define "Spine2" do |device|
    
    device.vm.hostname = "Spine2" 
    
    device.vm.box = "CumulusCommunity/cumulus-vx"
    device.vm.provider "virtualbox" do |v|
      v.name = "Spine2"
      v.customize ["modifyvm", :id, '--audiocontroller', 'AC97', '--audio', 'Null']
      v.memory = 1024
    end
    
    device.vm.synced_folder ".", "/vagrant", disabled: true
	
    # NETWORK INTERFACES
      # link for swp1 --> to_Leaf1
      device.vm.network "private_network", virtualbox__intnet: "sw_L1SP2", auto_config: false , :mac => "a00000000022"
      # link for swp2 --> to_Leaf2
      device.vm.network "private_network", virtualbox__intnet: "sw_L2SP2", auto_config: false , :mac => "44383900002b"
      # link for swp3 --> to_Leaf3
      device.vm.network "private_network", virtualbox__intnet: "sw_L3SP2", auto_config: false , :mac => "443839000068"
      # link for swp4 --> to_Leaf4
      device.vm.network "private_network", virtualbox__intnet: "sw_L4SP2", auto_config: false , :mac => "443839000020"
	  
    device.vm.provider "virtualbox" do |vbox|
      vbox.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', "--nictype2", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all', "--nictype3", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc4', 'allow-all', "--nictype4", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc5', 'allow-all', "--nictype5", "virtio"]
      vbox.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end
    
    # Run Any Extra Config
    device.vm.provision :shell , path: "./helper_scripts/config_Spine2.sh"	

end

  ##### DEFINE VM for Leaf1 #####
  config.vm.define "Leaf1" do |device|
    
    device.vm.hostname = "Leaf1" 
    
    device.vm.box = "CumulusCommunity/cumulus-vx"
    device.vm.provider "virtualbox" do |v|
      v.name = "Leaf1"
      v.customize ["modifyvm", :id, '--audiocontroller', 'AC97', '--audio', 'Null']
      v.memory = 1024
    end
    
    device.vm.synced_folder ".", "/vagrant", disabled: true
	
    # NETWORK INTERFACES
      # link for swp1 --> to_Server1
      device.vm.network "private_network", virtualbox__intnet: "sw_S1L1", auto_config: false , :mac => "a00000000011"
      # link for swp2 --> to_Spine1
      device.vm.network "private_network", virtualbox__intnet: "sw_L1SP1", auto_config: false , :mac => "443839000004"
      # link for swp3 --> to_Spine2
      device.vm.network "private_network", virtualbox__intnet: "sw_L1SP2", auto_config: false , :mac => "443839000016"
      # link for swp4 --> to_Leaf1_1
      device.vm.network "private_network", virtualbox__intnet: "sw_1L1L2", auto_config: false , :mac => "443839000021"
      # link for swp5 --> to_Leaf1_2
      device.vm.network "private_network", virtualbox__intnet: "sw_2L1L2", auto_config: false , :mac => "443839000022"
	  
    device.vm.provider "virtualbox" do |vbox|
      vbox.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', "--nictype2", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all', "--nictype3", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc4', 'allow-all', "--nictype4", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc5', 'allow-all', "--nictype5", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc6', 'allow-all', "--nictype6", "virtio"]
      #vbox.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end
	
    # Run Any Extra Config
    device.vm.provision :shell , path: "./helper_scripts/config_Leaf1.sh"
	
end

  ##### DEFINE VM for Leaf2 #####
  config.vm.define "Leaf2" do |device|
    
    device.vm.hostname = "Leaf2" 
    
    device.vm.box = "CumulusCommunity/cumulus-vx"
    device.vm.provider "virtualbox" do |v|
      v.name = "Leaf2"
      v.customize ["modifyvm", :id, '--audiocontroller', 'AC97', '--audio', 'Null']
      v.memory = 1024
    end
    
    device.vm.synced_folder ".", "/vagrant", disabled: true
	
    # NETWORK INTERFACES
      # link for swp1 --> to_Server1
      device.vm.network "private_network", virtualbox__intnet: "sw_S2L2", auto_config: false , :mac => "a00000000012"
      # link for swp2 --> to_Spine1
      device.vm.network "private_network", virtualbox__intnet: "sw_L2SP1", auto_config: false , :mac => "443839000018"
      # link for swp3 --> to_Spine2
      device.vm.network "private_network", virtualbox__intnet: "sw_L2SP2", auto_config: false , :mac => "44383900001c"
      # link for swp4 --> to_Leaf2_1
      device.vm.network "private_network", virtualbox__intnet: "sw_1L1L2", auto_config: false , :mac => "44383900000e"
      # link for swp5 --> to_Leaf2_2
      device.vm.network "private_network", virtualbox__intnet: "sw_2L1L2", auto_config: false , :mac => "44383900000f"
	  
    device.vm.provider "virtualbox" do |vbox|
      vbox.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', "--nictype2", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all', "--nictype3", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc4', 'allow-all', "--nictype4", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc5', 'allow-all', "--nictype5", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc6', 'allow-all', "--nictype6", "virtio"]
      vbox.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end
	
    # Run Any Extra Config
    device.vm.provision :shell , path: "./helper_scripts/config_Leaf2.sh"
	
end

  ##### DEFINE VM for Leaf3 #####
  config.vm.define "Leaf3" do |device|
    
    device.vm.hostname = "Leaf3" 
    
    device.vm.box = "CumulusCommunity/cumulus-vx"
    device.vm.provider "virtualbox" do |v|
      v.name = "Leaf3"
      v.customize ["modifyvm", :id, '--audiocontroller', 'AC97', '--audio', 'Null']
      v.memory = 1024
    end
    
    device.vm.synced_folder ".", "/vagrant", disabled: true
	
    # NETWORK INTERFACES
      # link for swp1 --> to_Server2
      device.vm.network "private_network", virtualbox__intnet: "sw_S2L3", auto_config: false , :mac => "a00000000013"
      # link for swp2 --> to_Spine1
      device.vm.network "private_network", virtualbox__intnet: "sw_L3SP1", auto_config: false , :mac => "443839000029"
      # link for swp3 --> to_Spine2
      device.vm.network "private_network", virtualbox__intnet: "sw_L3SP2", auto_config: false , :mac => "443839000024"
      # link for swp4 --> to_Leaf3_1
      device.vm.network "private_network", virtualbox__intnet: "sw_1L3L4", auto_config: false , :mac => "443839000030"
      # link for swp5 --> to_Leaf3_2
      device.vm.network "private_network", virtualbox__intnet: "sw_2L3L4", auto_config: false , :mac => "443839000031"
	  
    device.vm.provider "virtualbox" do |vbox|
      vbox.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', "--nictype2", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all', "--nictype3", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc4', 'allow-all', "--nictype4", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc5', 'allow-all', "--nictype5", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc6', 'allow-all', "--nictype6", "virtio"]
      vbox.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end
	
    # Run Any Extra Config
    device.vm.provision :shell , path: "./helper_scripts/config_Leaf3.sh"
	
end

  ##### DEFINE VM for Leaf4 #####
  config.vm.define "Leaf4" do |device|
    
    device.vm.hostname = "Leaf4" 
    
    device.vm.box = ""
    device.vm.provider "virtualbox" do |v|
      v.name = "Leaf4"
      v.customize ["modifyvm", :id, '--audiocontroller', 'AC97', '--audio', 'Null']
      v.memory = 1024
    end
    
    device.vm.synced_folder ".", "/vagrant", disabled: true
	
    # NETWORK INTERFACES
      # link for swp1 --> to_Server2
      device.vm.network "private_network", virtualbox__intnet: "sw_S2L4", auto_config: false , :mac => "a00000000014"
      # link for swp2 --> to_Spine1
      device.vm.network "private_network", virtualbox__intnet: "sw_L4SP1", auto_config: false , :mac => "443839000066"
      # link for swp3 --> to_Spine2
      device.vm.network "private_network", virtualbox__intnet: "sw_L4SP2", auto_config: false , :mac => "443839000033"
      # link for swp4 --> to_Leaf4_1
      device.vm.network "private_network", virtualbox__intnet: "sw_1L3L4", auto_config: false , :mac => "44383900001d"
      # link for swp5 --> to_Leaf4_2
      device.vm.network "private_network", virtualbox__intnet: "sw_2L3L4", auto_config: false , :mac => "44383900001e"
	  
    device.vm.provider "virtualbox" do |vbox|
      vbox.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', "--nictype2", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all', "--nictype3", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc4', 'allow-all', "--nictype4", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc5', 'allow-all', "--nictype5", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc6', 'allow-all', "--nictype6", "virtio"]
      vbox.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end
	
    # Run Any Extra Config
    device.vm.provision :shell , path: "./helper_scripts/config_Leaf4.sh"
	
end

  ##### DEFINE VM for Server1 #####
  config.vm.define "Server1" do |device|
    
    device.vm.hostname = "Server1" 
    
    device.vm.box = "CumulusCommunity/cumulus-vx"
    device.vm.provider "virtualbox" do |v|
      v.name = "Server1"
      v.customize ["modifyvm", :id, '--audiocontroller', 'AC97', '--audio', 'Null']
      v.memory = 1024
    end
    
    device.vm.synced_folder ".", "/vagrant", disabled: true
	
    # NETWORK INTERFACES
      # link for swp1 --> to_Leaf1
      device.vm.network "private_network", virtualbox__intnet: "sw_S1L1", auto_config: false , :mac => "a00000000031"
      # link for swp2 --> to_Leaf2
      device.vm.network "private_network", virtualbox__intnet: "sw_S2L2", auto_config: false , :mac => "443839000003"
      
	  
    device.vm.provider "virtualbox" do |vbox|
      vbox.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', "--nictype2", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all', "--nictype3", "virtio"]
      vbox.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end
	
    # Run Any Extra Config
    device.vm.provision :shell , path: "./helper_scripts/config_Server1.sh"
	
end

  ##### DEFINE VM for Server2 #####
  config.vm.define "Server2" do |device|
    
    device.vm.hostname = "Server2" 
    
    device.vm.box = "CumulusCommunity/cumulus-vx"
    device.vm.provider "virtualbox" do |v|
      v.name = "Server2"
      v.customize ["modifyvm", :id, '--audiocontroller', 'AC97', '--audio', 'Null']
      v.memory = 1024
    end
    
    device.vm.synced_folder ".", "/vagrant", disabled: true
	
    # NETWORK INTERFACES
      # link for swp1 --> to_Leaf3
      device.vm.network "private_network", virtualbox__intnet: "sw_S2L3", auto_config: false , :mac => "a00000000033"
      # link for swp2 --> to_Leaf4
      device.vm.network "private_network", virtualbox__intnet: "sw_S2L4", auto_config: false , :mac => "443839000028"
      
	  
    device.vm.provider "virtualbox" do |vbox|
      vbox.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', "--nictype2", "virtio"]
      vbox.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all', "--nictype3", "virtio"]
      vbox.customize ["modifyvm", :id, "--nictype1", "virtio"]
    end
	
    # Run Any Extra Config
    device.vm.provision :shell , path: "./helper_scripts/config_Server2.sh"
	
end

end
