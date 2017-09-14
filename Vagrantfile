VAGRANTFILE_API_VERSION = "2"
IGNITION_CONFIG_PATH = File.join(File.dirname(__FILE__), "config.ign")

$num_instances = 3

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|      
  config.ssh.insert_key = false
  config.ssh.forward_agent = true
  config.vm.box = "coreos-alpha"  
  config.vm.box_url = "https://alpha.release.core-os.net/amd64-usr/current/coreos_production_vagrant_virtualbox.json"
  
  ["vmware_fusion", "vmware_workstation"].each do |vmware|
    config.vm.provider vmware do |v, override|
      override.vm.box_url = "https://alpha.release.core-os.net/amd64-usr/current/coreos_production_vagrant_vmware_fusion.json"
    end
  end

  config.vm.provider :virtualbox do |v|
    # On VirtualBox, we don't have guest additions or a functional vboxsf
    # in CoreOS, so tell Vagrant that so it can be smarter.
    v.check_guest_additions = false
    v.functional_vboxsf     = false
    # enable ignition (this is always done on virtualbox as this is how the ssh key is added to the system)
    config.ignition.enabled = true
  end

  # plugin conflict
  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = false
  end  

  config.vm.network "private_network", type: "dhcp"

  (1..$num_instances).each do |instance_number|
    name = instance_number == 1 ? "manager" : "worker"
    config.vm.define vm_name = "#{name}-#{instance_number}" do |host|
      
      host.vm.hostname = "#{name}-#{instance_number}"

      config.vm.provider :virtualbox do |vb|
        config.ignition.hostname = vm_name
        config.ignition.drive_name = "config" + instance_number.to_s
        # when the ignition config doesn't exist, the plugin automatically generates a very basic Ignition with the ssh key
        # and previously specified options (ip and hostname). Otherwise, it appends those to the provided config.ign below
        if File.exist?(IGNITION_CONFIG_PATH)
          config.ignition.path = 'config.ign'
        end
      end
    end
  end
end