# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.define "vm01" do |cfg|
    cfg.vm.hostname = "vm01"
    cfg.vm.network :public_network, ip: "10.0.42.10", bridge: "en0: Wi-Fi (AirPort)"

    cfg.vm.provision "shell",
                     run: "always",
                     inline: "route add default gw 10.0.42.20"
  end

  config.vm.define "vm02" do |cfg|
    cfg.vm.hostname = "vm02"
    cfg.vm.network :public_network, ip: "10.0.42.20", bridge: "en0: Wi-Fi (AirPort)"
    cfg.vm.provision "shell",
                     run: "always",
                     inline: "sysctl -w net.ipv4.ip_forward=1"

    cfg.vm.provision "shell",
                     run: "always",
                     inline: "iptables -t nat -A POSTROUTING ! -d 10.0.42.0/24 -o eth0 -j MASQUERADE"
  end

  config.vm.provider "virtualbox" do |v|
    v.linked_clone = true
  end
end
