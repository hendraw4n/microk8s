Vagrant.configure("2") do |config|
  config.vm.define "microk8s" do |microk8s|
    microk8s.vm.box = "ubuntu/bionic64"
    microk8s.vm.hostname = "microk8s"
    microk8s.vm.network "public_network", 
      use_dhcp_assigned_default_route: true

    microk8s.vm.provider "virtualbox" do |vb|
      vb.name = "microk8s"
      vb.memory = 4096
      vb.cpus = 2
    end
    
    microk8s.vm.provision "shell", inline: <<-EOF
      snap install microk8s --classic
      snap install docker
      microk8s.status --wait-ready
      microk8s.enable dns dashboard registry
      usermod -a -G microk8s vagrant
      echo "alias kubectl='microk8s.kubectl'" > /home/vagrant/.bash_aliases
      chown vagrant:vagrant /home/vagrant/.bash_aliases
      echo "alias kubectl='microk8s.kubectl'" > /root/.bash_aliases
      chown root:root /root/.bash_aliases
    EOF
  end
end