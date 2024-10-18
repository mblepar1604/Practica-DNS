Vagrant.configure("2") do |config|
  
  config.vm.box = "debian/bookworm64"
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y bind9
  SHELL

  config.vm.define "venus" do |venus| #slave
    venus.vm.network "private_network", ip: "192.168.57.102"
  end
  
  config.vm.define "tierra" do |tierra| #master
    tierra.vm.network "private_network", ip: "192.168.57.103"
  end
end
