Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["E:\\Home\\Projects\\VagrantConfigMgmt\\keys\\private", "~/.vagrant.d/insecure_private_key"]
  # Prevent Vagrant from mounting the default /vagrant synced folder
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 256
    vb.cpus = 1
  end

  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "centos/7"
    ansible.vm.hostname = "ansible"
    ansible.vm.network "private_network",
							virtualbox__intnet: 'internal',
              ip: "192.168.33.10"
    ansible.vm.provision "file", source: "E:\\Home\\Projects\\VagrantConfigMgmt\\keys\\public", destination: "~/.ssh/authorized_keys" 
    ansible.vm.provision "shell", inline: <<-EOC
    localectl set-keymap uk
	  sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
	  systemctl restart sshd
	  yum install screen mlocate zip unzip epel-release bind-utils net-tools git policycoreutils-python libsemanage-python syslinux-tftpboot tcpdump wget -y
	  echo autocmd FileType yaml setlocal ai ts=2 sw=2 et > /home/vagrant/.vimrc
	  echo "192.168.33.10  ansible.localnet  ansible.localnet" >> /etc/hosts
    echo "192.168.33.11  centos1  centos1.localnet" >> /etc/hosts
    echo "192.168.33.12  centos2  centos2.localnet" >> /etc/hosts
    echo "192.168.33.13  centos3  centos3.localnet" >> /etc/hosts
    yum install python2-pip -y
    pip install ansible ansible-vault ansible-windows-compat pyvmomi
    pip install pywinrm[credssp]
	  EOC
  end

  config.vm.define "centos1" do |centos1|
    centos1.vm.box = "centos/7"
    centos1.vm.hostname = "centos1"
    centos1.vm.network "private_network",
							virtualbox__intnet: 'internal',
              ip: "192.168.33.11"
    centos1.vm.provision "file", source: "E:\\Home\\Projects\\VagrantConfigMgmt\\keys\\public", destination: "~/.ssh/authorized_keys" 
    centos1.vm.provision "shell", inline: <<-EOC
	  localectl set-keymap uk
	  sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
	  systemctl restart sshd
	  yum install screen mlocate zip unzip epel-release bind-utils net-tools git policycoreutils-python libsemanage-python syslinux-tftpboot tcpdump wget -y
	  echo autocmd FileType yaml setlocal ai ts=2 sw=2 et > /home/vagrant/.vimrc
	  echo "192.168.33.10  ansible.localnet  ansible.localnet" >> /etc/hosts
    echo "192.168.33.11  centos1  centos1.localnet" >> /etc/hosts
    echo "192.168.33.12  centos2  centos2.localnet" >> /etc/hosts
    echo "192.168.33.13  centos3  centos3.localnet" >> /etc/hosts
	  EOC
  end

  config.vm.define "centos2" do |centos2|
    centos2.vm.box = "centos/7"
    centos2.vm.hostname = "centos2"
    centos2.vm.network "private_network",
							virtualbox__intnet: 'internal',
              ip: "192.168.33.12"
    centos2.vm.provision "file", source: "E:\\Home\\Projects\\VagrantConfigMgmt\\keys\\public", destination: "~/.ssh/authorized_keys" 
    centos2.vm.provision "shell", inline: <<-EOC
	  localectl set-keymap uk
	  sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
	  systemctl restart sshd
	  yum install screen mlocate zip unzip epel-release bind-utils net-tools git policycoreutils-python libsemanage-python syslinux-tftpboot tcpdump wget -y
	  echo autocmd FileType yaml setlocal ai ts=2 sw=2 et > /home/vagrant/.vimrc
	  echo "192.168.33.10  ansible.localnet  ansible.localnet" >> /etc/hosts
    echo "192.168.33.11  centos1  centos1.localnet" >> /etc/hosts
    echo "192.168.33.12  centos2  centos2.localnet" >> /etc/hosts
    echo "192.168.33.13  centos3  centos3.localnet" >> /etc/hosts
	  EOC
  end

  config.vm.define "win1" do |win1|
    win1.vm.guest = :windows
    win1.vm.box = "opentable/win-2012r2-standard-amd64-nocm"
    win1.vm.hostname = "win1"
    win1.vm.network "private_network",
              virtualbox__intnet: 'internal',
              ip: "192.168.33.13"
  end

  config.vm.define "win2" do |win2|
    win2.vm.box = "opentable/win-2012r2-standard-amd64-nocm"
    win2.vm.hostname = "win2"
    win2.vm.network "private_network",
              virtualbox__intnet: 'internal',
              ip: "192.168.33.14"
  end
end