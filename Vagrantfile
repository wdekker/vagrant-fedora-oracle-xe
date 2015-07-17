# -*- mode: ruby -*-
# vi: set ft=ruby :
$script = <<SCRIPT

if [ ! -f /vagrant/oracle-xe-11.2.0*.rpm.zip ]; then
  echo 'Installation failed!'
  echo 'No Oracle XE installation zip (oracle-xe-11.2.0*.rpm.zip) is present.'
  echo 'Please download and put in the folder next to the Vagrantfile.'
  echo 'Run vagrant provision to resume'
  exit -1
fi

echo Resizing swap to 2048M as requested by Oracle XE
lvresize /dev/vg_vagrant/lv_root -f -l -21
swapoff -v /dev/vg_vagrant/lv_swap 
lvresize /dev/vg_vagrant/lv_swap -f -L 2048M
swapon -v /dev/vg_vagrant/lv_swap 

echo Installing bc and unzip for installing Oracle XE
yum -y install bc
yum -y install unzip

echo Installing Oracle XE
unzip /vagrant/oracle-xe-11.2.0*.rpm.zip -d /home/vagrant/oracle
rpm -ivh /home/vagrant/oracle/Disk1/oracle-xe-11.2.0*.rpm
rm -rf /home/vagrant/oracle
/etc/init.d/oracle-xe configure responseFile=/vagrant/xe.rsp
/etc/init.d/oracle-xe start
echo Setup Oracle environment
. /u01/app/oracle/product/11.2.0/xe/bin/oracle_env.sh
echo '. /u01/app/oracle/product/11.2.0/xe/bin/oracle_env.sh' >> /home/vagrant/.bash_profile

if [ ! -f /vagrant/postinstall.sh ]; then
  echo 'No optional /vagrant/postinstall.sh file found, skipping.'
else
  echo 'Running optional postinall script'
  sh /vagrant/postinstall.sh
fi  

SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "chef/fedora-21"

  config.vm.network "forwarded_port", guest: 1521, host: 1521

  config.vm.provision "shell", inline: $script
end
