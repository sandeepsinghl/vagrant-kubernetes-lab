Vagrant.configure("2") do |config|

    # ==========================================
    # GLOBAL SETTINGS (Applied to all nodes)
    # ==========================================
    # Disable default VirtualBox shared folders to support native WSL execution
    config.vm.synced_folder ".", "/vagrant", disabled: true

    # ==========================================
    # 1. KUBERNETES MASTER NODE
    # ==========================================
    config.vm.define "k8s-master" do |master|
      master.vm.box = "ubuntu/jammy64"
      master.vm.hostname = "k8s-master"
      master.vm.network "private_network", ip: "192.168.56.10"
      
      master.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = 2048
      end
    end
  
    # ==========================================
    # 2. KUBERNETES WORKER NODE 1
    # ==========================================
    config.vm.define "k8s-worker-1" do |worker1|
      worker1.vm.box = "ubuntu/jammy64"
      worker1.vm.hostname = "k8s-worker-1"
      worker1.vm.network "private_network", ip: "192.168.56.11"
      
      worker1.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = 2048
      end

      # ==========================================
      # 3. HOST-BASED ANSIBLE PROVISIONER
      # ==========================================
      # Executed locally from WSL after both VMs are fully initialized.
      # This automatically generates the dynamic 'hosts' inventory file on your desktop.
      worker1.vm.provision "ansible" do |ansible|
        ansible.playbook = "cluster-setup.yml"
        ansible.inventory_path = "hosts"
        ansible.groups = {
          "masters" => ["k8s-master"],
          "workers" => ["k8s-worker-1"],
          "k8s_cluster:children" => ["masters", "workers"]
        }
      end
    end
end