Vagrant.configure("2") do |config|

    config.vm.define "ansible" do |ansible|
        ansible.vm.box = "ubuntu/bionic64"
        ansible.vm.network "private_network", ip: "172.17.177.40"
        ansible.vm.provider "virtualbox" do |vba|
            
            vba.memory = 1024
            vba.cpus = 2
            vba.name = "ansible base"
        end

        # Copiando as chaves SSH para a pasta ~ do Ubuntu
        ansible.vm.provision "shell", inline: "cp /vagrant/files/ansible.pub /home/vagrant"
        ansible.vm.provision "shell", inline: "cp /vagrant/files/ansible /home/vagrant"

        # Copiando os arquivos usados pelo Ansible para a pasta ~ do Ubuntu
        ansible.vm.provision "shell", inline: "cp /vagrant/files/000-default.conf /home/vagrant/000-default.conf"
        ansible.vm.provision "shell", inline: "cp /vagrant/files/hosts /home/vagrant/hosts"
        ansible.vm.provision "shell", inline: "cp /vagrant/files/provisioning.yml /home/vagrant/provisioning.yml"
        ansible.vm.provision "shell", inline: "cp -r /vagrant/files/group_vars /home/vagrant/"
        ansible.vm.provision "shell", inline: "cp -r /vagrant/files/roles /home/vagrant/"
        ansible.vm.provision "shell", inline: "cp -r /vagrant/files/templates /home/vagrant/"

        # Alterando o owner e as permissões para as chaves SSH
        ansible.vm.provision "shell", inline: "chmod 600 /home/vagrant/ansible.pub"
        ansible.vm.provision "shell", inline: "chmod 600 /home/vagrant/ansible"
        ansible.vm.provision "shell", inline: "chown vagrant:vagrant /home/vagrant/ansible.pub"
        ansible.vm.provision "shell", inline: "chown vagrant:vagrant /home/vagrant/ansible"

        # Alterando o owner e as permissões para os arquivos do Ansible
        ansible.vm.provision "shell", inline: "chmod 600 /home/vagrant/000-default.conf"
        ansible.vm.provision "shell", inline: "chmod 700 /home/vagrant/group_vars/"
        ansible.vm.provision "shell", inline: "chmod 600 /home/vagrant/group_vars/all.yml"
        ansible.vm.provision "shell", inline: "chmod 600 /home/vagrant/hosts"
        ansible.vm.provision "shell", inline: "chmod 600 /home/vagrant/provisioning.yml"
        ansible.vm.provision "shell", inline: "chown vagrant:vagrant /home/vagrant/000-default.conf"
        ansible.vm.provision "shell", inline: "chown -R vagrant:vagrant /home/vagrant/group_vars"
        ansible.vm.provision "shell", inline: "chown vagrant:vagrant /home/vagrant/hosts"
        ansible.vm.provision "shell", inline: "chown vagrant:vagrant /home/vagrant/provisioning.yml"

        # Permitindo acesso com ssh
        ansible.vm.provision "shell", inline: "cat /vagrant/files/ansible.pub >> .ssh/authorized_keys"

        # Atualizando o apt-get e instalando o Ansible
        ansible.vm.provision "shell", inline: "sudo apt-get update"
        ansible.vm.provision "shell", inline: "sudo apt-get install ansible -y"
    end

    config.vm.define "wordpress" do |wordpress|
        wordpress.vm.box = "ubuntu/bionic64"

        wordpress.vm.network "private_network", ip: "172.17.177.41"
        wordpress.vm.provider "virtualbox" do |vbw|
            
            vbw.memory = 1024
            vbw.cpus = 2
            vbw.name = "wordpress server"
        end

        wordpress.vm.provision "shell", inline: "cat /vagrant/files/ansible.pub >> .ssh/authorized_keys"
    end

    config.vm.define "mysql" do |mysql|
        mysql.vm.box = "ubuntu/bionic64"

        mysql.vm.network "private_network", ip: "172.17.177.42"
        mysql.vm.provider "virtualbox" do |vbmy|
            
            vbmy.memory = 1024
            vbmy.cpus = 2
            vbmy.name = "mysql server"
        end

        mysql.vm.provision "shell", inline: "cat /vagrant/files/ansible.pub >> .ssh/authorized_keys"
    end
end