Vagrant.configure("2") do |config|
  
  config.vm.box = "debian/bookworm64"
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y bind9
  SHELL

  config.vm.define "venus" do |venus| #slave
    venus.vm.network "private_network", ip: "192.168.57.102"
    venus.vm.provision "shell", inline: <<-SHELL
      sudo su
      cp -v /vagrant/files/named /etc/default
      cp -v /vagrant/files/named.conf.options /etc/bind
      cp -v /vagrant/files/slavenamed.conf.local /etc/bind/named.conf.local

      systemctl reload named
      systemctl status named
    SHELL
  end
  
  config.vm.define "tierra" do |tierra| #master
    tierra.vm.network "private_network", ip: "192.168.57.103"
    tierra.vm.provision "shell", inline: <<-SHELL
    sudo su
      cp -v /vagrant/files/named /etc/default
      cp -v /vagrant/files/named.conf.options /etc/bind
      cp -v /vagrant/files/masternamed.conf.local /etc/bind/named.conf.local
      cp -v /vagrant/files/master.sistema.test.dns /var/lib/bind/db.sistema.test
      cp -v /vagrant/files/master.sistema.test.inverso.dns /var/lib/bind/db.sistema.test.rev

      systemctl reload named
      systemctl status named
    SHELL
  end
end
