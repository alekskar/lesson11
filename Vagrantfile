Vagrant.configure("2") do |config|
  config.vm.define "puppet_server", primary: true do |web|
    web.vm.box = "sbeliakou/centos-6.7-x86_64"
    web.vm.hostname = "puppetserver"
    web.vm.network "private_network", ip: "192.168.100.116"
    web.vm.provider "virtualbox" do |host|
	host.name="puppetserver"
	host.cpus = 2
	host.memory = 4234 
	end
    web.vm.provision "shell", inline: <<-SHELL
echo "192.168.100.116   puppetserver puppetserver.minsk.epam.com" >> /etc/hosts
echo "192.168.100.117   puppetstandalone puppetstandalone.minsk.epam.com" >> /etc/hosts
rpm -ihv https://yum.puppetlabs.com/puppetlabs-release-pc1-el-6.noarch.rpm
#yum install -y puppetserver
SHELL
  end
  config.vm.define "puppet_standalone", primary: true do |web|
    web.vm.box = "sbeliakou/centos-6.7-x86_64"
    web.vm.hostname = "puppetstandalone"
    web.vm.network "private_network", ip: "192.168.100.117"
    web.vm.provider "virtualbox" do |host|
        host.name="puppetstandalone"
        host.cpus = 1
        host.memory = 768
        end
    web.vm.provision "shell", inline: <<-SHELL
echo "192.168.100.116  puppetserver puppetserver.minsk.epam.com" >> /etc/hosts
echo "192.168.100.117  puppetstandalone puppetstandalone.minsk.epam.com" >> /etc/hosts
rpm -ihv https://yum.puppetlabs.com/puppetlabs-release-pc1-el-6.noarch.rpm
yum install -y puppet
SHELL
  end

config.vm.provision "shell", inline: <<-SHELL
echo "This host is ready for provisioning" 
SHELL
end
