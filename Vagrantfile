Vagrant.configure(2) do |config|
 
  config.vm.box = "opentable/win-2012r2-standard-amd64-nocm"
  config.vm.guest = :windows
  config.vm.communicator = "winrm"
  
  config.vm.provision :shell, path: "scripts/install-iis.cmd"
 
  config.vm.boot_timeout = 600
 
  config.vm.define "web" do |web|
    web.vm.network "private_network", ip: "192.168.56.202"
    web.vm.host_name = "IIS"
    web.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
    web.vm.provision :shell, path: "scripts/install-iis.cmd"
  end
 
  config.vm.define "sql" do |sql|
    sql.vm.network "private_network", ip: "192.168.56.203"
    sql.vm.host_name = "sql"
    sql.vm.network :forwarded_port, guest: 5985, host: 5986, id: "winrm", auto_correct: true
  end
 

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
     vb.gui = true

    vb.cpus = 2
    vb.memory = 2048
  end
 
end