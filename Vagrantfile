Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
	end
  config.vm.box = "ubuntu/xenial64"
  config.vm.define "mgr" do |mgr|
    mgr.vm.hostname = "mgr.site"
    if ENV['ENV'] != 'local'
      mgr.vm.network "public_network", ip: "192.168.5.10"
    else
      mgr.vm.network "private_network", ip: "192.168.5.10",
        virtualbox__intnet: "piNetwork"
    end
    mgr.vm.provision "docker" do |d|
      d.post_install_provision "shell", path: "bootstrap.sh"
      d.run "jenkinsci/blueocean",
        args: "-d -p 8080:8080 -v /vagrant/jenkins:/var/jenkins_home "
    end
	end
end
