Vagrant.configure("2") do |config|

  servers=[
    {
      :hostname => "Web1",
      :box => "ubuntu/jammy64",
      :ip => "192.168.56.50",
      :ssh_port => '2200',
      :web_port => '8080'
    },
    {
      :hostname => "Web2",
      :box => "ubuntu/jammy64",
      :ip => "192.168.56.51",
      :ssh_port => '2201',
      :web_port => '8081'
    },{
      :hostname => "DB",
      :box => "ubuntu/jammy64",
      :ip => "192.168.56.52",
      :ssh_port => '2202'
    }
  ]

  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      node.vm.network :private_network, ip: machine[:ip]
      node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
      if machine[:web_port]
        node.vm.network "forwarded_port", guest: 80, host: machine[:web_port], id: "web"
      end

      node.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", 1024]
        vb.customize ["modifyvm", :id, "--cpus", 1]
      end
    end
  end
end