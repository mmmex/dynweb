Vagrant.configure(2) do |config|
    config.vm.define "dynweb" do |vmconfig|
        vmconfig.vm.box = 'bento/ubuntu-20.04'
        vmconfig.vm.hostname = 'dynweb'
        vmconfig.vm.network "forwarded_port", guest: 8083, host: 8083
        vmconfig.vm.network "forwarded_port", guest: 8081, host: 8081
        vmconfig.vm.network "forwarded_port", guest: 8082, host: 8082
        vmconfig.vm.provider "virtualbox" do |vbx|
            vbx.memory = "2048"
            vbx.cpus = "2"
            vbx.customize ["modifyvm", :id, '--audio', 'none']
        end
        vmconfig.vm.provision "ansible" do |ansible|
            ansible.playbook = "provision.yml"
        end
        
    end
end
    