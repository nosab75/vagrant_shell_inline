NETWORK_ADAPTER="Killer E2600 Gigabit Ethernet Controller"  # Bridge network adapter

Vagrant.configure("2") do |config|
   config.vm.define "server1" do |srv1|
    srv1.vm.box = "nercceh/ubuntu20.04"
    srv1.vm.hostname = 'ubuntu'
    srv1.vm.network :public_network, bridge: NETWORK_ADAPTER, ip: "192.168.1.98"
    srv1.vm.box_download_insecure=true
   end

   config.vm.define "server2" do |srv2|
    srv2.vm.box = "centos/8"
    srv2.vm.hostname = 'centos'
    srv2.vm.box_download_insecure=true
    srv2.vm.network :public_network, bridge: NETWORK_ADAPTER, ip: "192.168.1.99"

    srv2.vm.provision "shell", inline: <<-SHELL
        sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
        systemctl restart sshd
      SHELL
   end

   # Fournisseur
   config.vm.provider "virtualbox" do |v|
     # v.gui = true
     v.memory = 1024
     v.cpus = 1
   end
end
