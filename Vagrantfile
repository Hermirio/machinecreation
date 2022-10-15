Vagrant.configure("2") do |config|
    config.vm.define "main" do |main|
        main.vm.box = "hashicorp/bionic64"
        main.vm.hostname = "main"
        main.vm.network "public_network", bridge: "wlp3s0", ip: "192.168.10.30"
        main.vm.provider "virtualbox" do |vb|
            vb.name = "main"
            vb.memory = 1024
            vb.cpus = 1
        end
    end

    (1..3).each do |num|
        config.vm.define "nodes_#{num}" do |nodes|
            nodes.vm.box = "hashicorp/bionic64"
            nodes.vm.hostname = "nodes#{num}"
            nodes.vm.network "public_network", bridge: "wlp3s0", ip: "192.168.10.3#{num}"
            nodes.vm.provider "virtualbox" do |vb|
                vb.name = "nodes_#{num}"
                vb.memory = 1024
                vb.cpus = 1
            end
        end
    end
    config.vm.provision "shell" do |ssh|
        ssh_pub_key = File.readlines("/home/whermirio/.ssh/id_rsa.pub").first.strip
        ssh.inline = <<-SHELL
            echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
            # echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
        SHELL
    end
end