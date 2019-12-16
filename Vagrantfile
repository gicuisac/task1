Vagrant.configure("2") do |config|

# VM"s base image
  config.vm.box = "centos/8"
# Provisioner definition
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
  end
# VM"s definition
  config.vm.define "lb1" do |lb|
    lb.vm.synced_folder "config/lb", "/opt/config", type: "nfs"
    lb.vm.network :forwarded_port, host: 8080, guest: 8080
    lb.vm.network :forwarded_port, host: 10443, guest: 443
    lb.vm.network :private_network, :ip => "192.168.111.10"
    lb.vm.hostname = "lb1"
    lb.vm.provider :virtualbox do |vb|
      vb.name = "lb1"
      vb.memory = 1024
      vb.cpus = 1
    end
  end

  (1..2).each do |i|
    config.vm.define "web#{i}" do |web|
      web.vm.synced_folder "hello-world.com", "/opt/hello-world.com", type: "nfs"
      web.vm.synced_folder "config/web#{i}", "/opt/config", type: "nfs"
      web.vm.network :private_network, :ip => "192.168.111.1#{i}"
      web.vm.hostname = "web#{i}"
      web.vm.provider :virtualbox do |vb|
        vb.name = "web#{i}"
        vb.memory = 1024
        vb.cpus = 1
      end
    end
  end
end