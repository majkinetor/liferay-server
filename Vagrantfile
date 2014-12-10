PROXY  = ENV['http_proxy']
PUBLIC = true

Vagrant.configure("2") do |cfg|
    cfg.vm.box = "utopic"
    cfg.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/utopic/current/utopic-server-cloudimg-amd64-vagrant-disk1.box"
    cfg.vm.network "public_network" if PUBLIC

    cfg.vm.define 'liferay' do |c|
        c.vm.hostname = 'liferay'

        #c.vm.forward_port 8080, 7991
        #c.vm.network :forwarded_port, guest:7991, host:8080

        c.vm.network "private_network", ip: "192.168.0.20" if !PUBLIC

        c.vm.provider "virtualbox" do |v|
            v.name = c.vm.hostname
            v.memory = 2048
            v.cpus = 2
        end

        c.vm.provision "shell", inline: <<-eos
            sed 's/^PermitRootLogin.*$/PermitRootLogin yes/'                   -i /etc/ssh/sshd_config
            service ssh restart
        eos

        cfg.vbguest.auto_update = false if Vagrant.has_plugin?("vagrant-vbguest")
    end

    cfg.vm.define 'ansible-master' do |c|
        c.vm.hostname = 'ansible-master'
        c.vm.synced_folder "ansible", "/ansible", :mount_options => ["dmode=777", "fmode=666"]
        c.vm.provider "virtualbox" do |v|
            v.name = c.vm.hostname
            v.memory = 2048
            v.cpus = 2
        end

        c.vm.provision "shell", inline: <<-eos
            apt-get update && apt-get -y install ansible sshpass
        eos
    end

    if Vagrant.has_plugin?("vagrant-proxyconf") and PROXY != nil
        puts "==| Setting proxy to #{PROXY}"
        cfg.proxy.http, cfg.proxy.https, cfg.proxy.ftp = [PROXY]*3
        cfg.proxy.no_proxy = "localhost,127.0.0.1"
    end
end
