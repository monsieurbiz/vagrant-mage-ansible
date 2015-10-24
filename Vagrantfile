# vi: set ft=ruby expandtab tabstop=2 :

hostname = "mage.dev"
virtualbox_ip = "192.168.10.42"

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Hostmanager default config
  # Using the hostmanager plugin. If missing, install it:
  #   vagrant plugin install vagrant-hostmanager
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  config.vm.define hostname do |node|

    # VMWare Fusion customization
    node.vm.provider :vmware_fusion do |vmware, override|

      # Which box?
      override.vm.box = "puphpet/debian75-x64"
      override.vm.box_url = "puphpet/debian75-x64"

      # Customize VM
      vmware.vmx["memsize"] = "1024"
      vmware.vmx["numvcpus"] = "1"

      # Network
      vmware.vmx["ethernet1.present"] = "TRUE"
      vmware.vmx["ethernet1.connectionType"] = "hostonly"
      vmware.vmx["ethernet1.virtualDev"] = "e1000"
      vmware.vmx["ethernet1.wakeOnPcktRcv"] = "FALSE"
      vmware.vmx["ethernet1.addressType"] = "generated"

    end

    # Virtualbox customization
    node.vm.provider :virtualbox do |virtualbox, override|

      # Customize VM
      virtualbox.customize ["modifyvm", :id, "--memory", "1024", "--cpus", "1", "--pae", "on", "--hwvirtex", "on", "--ioapic", "on"]

      # Network
      override.vm.network :private_network, ip: virtualbox_ip

    end

    # Network
    node.vm.hostname = hostname

    # Synced folders
    # On OSX we use some tips to boost the nfs ;)
    if (/darwin/ =~ RUBY_PLATFORM)
      node.vm.synced_folder "", "/vagrant", nfs: true,
        mount_options: ["nolock", "async"],
        bsd__nfs_options: ["alldirs","async","nolock"]
    else
      node.vm.synced_folder "", "/vagrant", nfs: true,
        mount_options: ["nolock", "async"]
    end

    # "Provision" with hostmanager
    node.vm.provision :hostmanager

      # Provision with Ansible
      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
        ansible.groups = {
          "vagrant" => [hostname]
        }
      end

  end

end

