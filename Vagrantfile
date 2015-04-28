    # -*- mode: ruby -*-lab
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.ssh.forward_agent = true

  config.vm.define "elkserver" do |elkserver|
    elkserver.vm.box = "frntn/trusty64-elk"
    elkserver.vm.network "private_network", ip: "192.168.34.150"
    elkserver.vm.network :forwarded_port, guest:9200, host: 9200
    elkserver.vm.network :forwarded_port, guest:9300, host: 9300
    elkserver.vm.network :forwarded_port, guest:80, host: 8080
    elkserver.vm.provision "file", source: "./UnlimitedJCEPolicyJDK7/local_policy.jar", destination: "/tmp/local_policy.jar"
    elkserver.vm.provision "file", source: "./UnlimitedJCEPolicyJDK7/US_export_policy.jar", destination: "/tmp/US_export_policy.jar"
    elkserver.vm.provision "file", source: "./nginx/default", destination: "/tmp/nginx-default"
    elkserver.vm.provision "shell", path: "elkserver-provision.sh"
    elkserver.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
    end
     
  end

  config.vm.define "elkclient" do |elkclient|
    elkclient.vm.box = "frntn/trusty64-wordpress"
    elkclient.vm.network "private_network", ip: "192.168.34.151"
    elkclient.vm.provision "shell", path: "elkclient-provision.sh"
  end

end
