# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX="centos/6"
NODES=2


# common initial script
$common_pg_init = <<SCRIPT
wget https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-6-x86_64/pgdg-centos96-9.6-3.noarch.rpm
yum install -y ./pgdg-centos96-9.6-3.noarch.rpm
yum install -y postgresql96-server postgres96
service postgresql-9.6 initdb
service postgresql-9.6 start
chkconfig postgresql-9.6 on
yum install -y install avahi
sudo service avahi-daemon start
chkconfig avahi-daemon on
SCRIPT

Vagrant.configure("2") do |config|
	(1..NODES).each do |i|
		config.vm.define "node#{i}" do |subconfig|
			subconfig.vm.box = BOX
			subconfig.vm.hostname = "node#{i}"
			subconfig.vm.provision "shell", inline: $common_pg_init
		end
	end 	
#	config.vm.provision "shell", inline: $common_pg_init
end
