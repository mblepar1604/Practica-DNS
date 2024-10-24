Vagrant.configure("2") do |config|
  
  config.vm.box = "debian/bookworm64"
  config.vm.provision "shell", name: "install_bind9", inline: <<-SHELL
    apt-get update
    apt-get install -y bind9
  SHELL
  config.vm.define "venus" do |venus| #slave
    venus.vm.network "private_network", ip: "192.168.57.102"
    venus.vm.provision "shell", name: "copiar_archivos_slave", inline: <<-SHELL
      sudo su
      cp -v /vagrant/files/comun/named /etc/default
      cp -v /vagrant/files/comun/named.conf.options /etc/bind
      cp -v /vagrant/files/slave/slavenamed.conf.local /etc/bind/named.conf.local
      cp -v /vagrant/files/slave/resolv.conf /etc

      systemctl reload bind9
      systemctl status bind9
    SHELL
  end
  
  config.vm.define "tierra" do |tierra| #master
    tierra.vm.network "private_network", ip: "192.168.57.103"
    tierra.vm.provision "shell", name: "crear_carpeta", inline: <<-SHELL
      sudo su
      mkdir -p /var/lib/bind
    SHELL
    tierra.vm.provision "shell", name: "copiar_archivos_master", inline: <<-SHELL
    sudo su
      cp -v /vagrant/files/comun/named /etc/default
      cp -v /vagrant/files/comun/named.conf.options /etc/bind
      cp -v /vagrant/files/master/masternamed.conf.local /etc/bind/named.conf.local
      cp -v /vagrant/files/master/master.sistema.test.dns /var/lib/bind/db.sistema.test
      cp -v /vagrant/files/master/master.sistema.test.inverso.dns /var/lib/bind/db.sistema.test.rev
      cp -v /vagrant/files/master/resolv.conf /etc

      # Cambiar permisos para que Bind pueda acceder a los archivos de zona
      chown bind:bind /var/lib/bind/db.sistema.test
      chown bind:bind /var/lib/bind/db.sistema.test.rev
      chmod 644 /var/lib/bind/db.sistema.test
      chmod 644 /var/lib/bind/db.sistema.test.rev


      systemctl reload bind9
      systemctl status bind9
    SHELL
  end
end
