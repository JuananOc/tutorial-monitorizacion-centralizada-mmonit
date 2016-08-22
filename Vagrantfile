# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/trusty64"

    config.vm.define "monit" do |monit|
        monit.vm.hostname = "monit"

        monit.vm.network :forwarded_port, host:  2222, guest: 22, id: "ssh"
        monit.vm.network :forwarded_port, host:  8888, guest: 80, id: "nginx"

        monit.vm.network :private_network, ip: "192.168.33.25"
    end

    config.vm.define "mmonit" do |mmonit|
        mmonit.vm.hostname = "mmonit"

        mmonit.vm.network :forwarded_port, host:  2223, guest: 22, id: "ssh"

        mmonit.vm.network :private_network, ip: "192.168.33.26"
    end

    config.vm.provision "ansible" do |ansible|
        ansible.verbose = 'vvv'
        ansible.playbook = "ansible/watchdog_nginx.yml"
    end
end
