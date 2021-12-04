Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
   config.vm.provider "virtualbox" do |vb|
     vb.memory = 2048
     vb.cpus = 1
   end


  config.vm.define "ansible" do |ab|
    ab.vm.network "public_network", ip: "192.168.1.147"
    ab.vm.provision "shell",
      inline: "apt-get install software-properties-common && \
               apt-add-repository ppa:ansible/ansible && \
               add-apt-repository ppa:ondrej/php && \
               apt-get update -y && \
               apt-get install -y ansible && \
               ssh-keygen -t rsa -f /vagrant/ssh-key/ansible -N '' <<< y
               "
    ab.vm.synced_folder ".", "/vagrant", disabled: true
    ab.vm.synced_folder ".", "/vagrant"
    ab.vm.synced_folder ".vagrant", "/vagrant/.vagrant"

  end

  config.vm.define "wordpress" do |wp|
    wp.vm.network "public_network", ip: "192.168.1.146"
    wp.vm.synced_folder ".", "/vagrant"
    wp.vm.synced_folder ".vagrant", "/vagrant/.vagrant"
    wp.vm.provision "shell",
    inline: "cat /vagrant/ssh-key/ansible.pub > ~/.ssh/authorized_keys"
  end


end
