Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  # Helps avoid SSH key issues with ubuntu/* boxes
  config.ssh.insert_key = false

  # nginx reverse proxy
  config.vm.define "nginx" do |vm|
    vm.vm.hostname = "nginx"
    vm.vm.network "private_network", ip: "192.168.56.10"
    vm.vm.network "public_network"

    vm.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end

    vm.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/site.yml"
      ansible.inventory_path = "ansible/inventory.ini"
      ansible.limit = "nginx"
      ansible.become = true
      ansible.verbose = "v"
    end
  end

  # postgres
  config.vm.define "postgres" do |vm|
    vm.vm.hostname = "postgres"
    vm.vm.network "private_network", ip: "192.168.56.12"

    vm.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end

    vm.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/site.yml"
      ansible.inventory_path = "ansible/inventory.ini"
      ansible.limit = "postgres"
      ansible.become = true
    end
  end

  # redmine (service, no docker)
  config.vm.define "redmine" do |vm|
    vm.vm.hostname = "redmine"
    vm.vm.network "private_network", ip: "192.168.56.11"

    vm.vm.provider "virtualbox" do |vb|
      vb.memory = 1536
      vb.cpus = 1
    end

    vm.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/site.yml"
      ansible.inventory_path = "ansible/inventory.ini"
      ansible.limit = "redmine"
      ansible.become = true
    end
  end

  # gitlab (omnibus)
  config.vm.define "gitlab" do |vm|
    vm.vm.hostname = "gitlab"
    vm.vm.network "private_network", ip: "192.168.56.13"

    vm.vm.provider "virtualbox" do |vb|
      vb.memory = 8192
      vb.cpus = 4
    end

    vm.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/site.yml"
      ansible.inventory_path = "ansible/inventory.ini"
      ansible.limit = "gitlab"
      ansible.become = true
    end
  end
end
