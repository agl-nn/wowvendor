VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.ssh.insert_key = false
    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "256"]
    end

    # ELK.
    config.vm.define "elk" do |elk|
        elk.vm.hostname = "elk"
        elk.vm.box = "centos/7"
        elk.vm.network :private_network, ip: "10.7.30.14"
        elk.vm.provider "virtualbox" do |vb|
            vb.memory = "2048"
            vb.cpus = "2"
        end
        elk.vm.provision "ansible" do |ansible|
           ansible.playbook = "elk.yml"
        end
     end
    # LB.
    config.vm.define "LB" do |lb|
        lb.vm.hostname = "LB"
        lb.vm.box = "centos/7"
	lb.vm.network :private_network, ip: "10.7.30.10"
	lb.vm.provision "ansible" do |ansible|
 	   ansible.playbook = "lb.yml"
        
	end
    end

    # NGINX 1.
    config.vm.define "nginx1" do |nginx|
        nginx.vm.hostname = "nginx1"
        nginx.vm.box = "centos/7"
        nginx.vm.network :private_network, ip: "10.7.30.11"
        nginx.vm.provision "ansible" do |ansible|
           ansible.playbook = "front.yml"
        end
    end


    # NGINX 2.
    config.vm.define "nginx2" do |nginx|
        nginx.vm.hostname = "nginx2"
        nginx.vm.box = "centos/7"
        nginx.vm.network :private_network, ip: "10.7.30.12"
        nginx.vm.provision "ansible" do |ansible|
           ansible.playbook = "front.yml"
        end
    end

    # NGINX HTML.
    config.vm.define "nginx-app" do |app|
        app.vm.hostname = "nginx-app"
        app.vm.box = "centos/7"
        app.vm.network :private_network, ip: "10.7.30.13"
	app.vm.provision "ansible" do |ansible|
           ansible.playbook = "app.yml"
        end
    end

end
