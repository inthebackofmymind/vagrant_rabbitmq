Vagrant.configure("2") do |config|

  config.vm.define "node1" do |node1|
    node1.vm.box = "bento/centos-7.2" 
    node1.vm.network "public_network", ip: "192.168.0.34"
    node1.vm.hostname = "node1"
  end

  config.vm.define "node2" do |node2|
    node2.vm.box = "bento/centos-7.2" 
    node2.vm.network "public_network", ip: "192.168.0.35"
    node2.vm.hostname = "node2"
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum -y update --exclude=kernel* 
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = 'rabbitmq.yml'
    ansible.groups = {
      "node1" => ["node1"],
      "node2" => ["node2"],
    }
  end
end
