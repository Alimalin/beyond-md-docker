
# Set an environment variable to disable parallel execution of Vagrant commands.
ENV['VAGRANT_NO_PARALLEL'] = 'yes'

# Define constants for Vagrant box and node configurations.
VAGRANT_BOX         = "generic/debian12"
CPUS_CONTROL_NODE   = 1
CPUS_WORKER_NODE    = 1
MEMORY_CONTROL_NODE = 1024
MEMORY_WORKER_NODE  = 1024
WORKER_NODES_COUNT  = 2

# Configure Vagrant with version 2.
Vagrant.configure(2) do |config|

  # Provision the VMs with a shell script (bootstrap.sh).
  #config.vm.provision "shell", path: "bootstrap.sh"



  # Define configurations for the control node.
  config.vm.define "docker-node" do |node|
  
    # Set the Vagrant box, disable box update checks, and set the hostname.
    node.vm.box               = VAGRANT_BOX
    node.vm.box_check_update  = false
    node.vm.hostname          = "docker.node.com"

    # Configure a private network with a specific IP address for the control node.
    node.vm.network "private_network", ip: "172.20.20.100"
    node.vm.network "forwarded_port", guest: 8080, host: 8080

  
    # Provider-specific configurations for VirtualBox.
    node.vm.provider :virtualbox do |v|
      v.name    = "control-node"
      v.memory  = MEMORY_CONTROL_NODE
      v.cpus    = CPUS_CONTROL_NODE
    end
  

  
    # Provision the control node with a shell script (control.sh).
    node.vm.provision "shell", path: "docker.sh"

    # Additional provisioning options (e.g., file sync, Ansible playbook execution) can be uncommented here.

  end

end
