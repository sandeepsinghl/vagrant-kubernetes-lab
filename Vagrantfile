Vagrant.configure("2") do |config|

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
    end
  
  end