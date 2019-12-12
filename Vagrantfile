Vagrant.configure("2") do |config|

# VM's base image
  config.vm.box = "centos/8"
# Provisioner definition
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
  end
# VM's definition
  config.vm.define "lb1" do |lb|
    lb.vm.synced_folder "config/lb", "/opt/config", type: "nfs"
    lb.vm.network :forwarded_port, host: 8080, guest: 8080
    lb.vm.network :forwarded_port, host: 10443, guest: 443
    lb.vm.network :private_network, :ip => '192.168.111.10'
    lb.vm.hostname = 'lb1'
    lb.vm.provider :virtualbox do |vb|
      vb.name = "lb1"
      vb.memory = 1024
      vb.cpus = 1
    end
  end

  config.vm.define "web1" do |web1|
    web1.vm.synced_folder "hello-world.com", "/opt/hello-world.com", type: "nfs"
    web1.vm.synced_folder "config/web1", "/opt/config", type: "nfs"
    web1.vm.network :private_network, :ip => '192.168.111.11'
    web1.vm.hostname = 'web1'
    web1.vm.provider :virtualbox do |vb|
      vb.name = "web1"
      vb.memory = 1024
      vb.cpus = 1
    end
  end

  config.vm.define "web2" do |web2|
    web2.vm.synced_folder "hello-world.com", "/opt/hello-world.com", type: "nfs"
    web2.vm.synced_folder "config/web2", "/opt/config", type: "nfs"
    web2.vm.network :private_network, :ip => '192.168.111.12'
    web2.vm.hostname = 'web2'
    web2.vm.provider :virtualbox do |vb|
      vb.name = "web2"
      vb.memory = 1024
      vb.cpus = 1
    end
  end
end
