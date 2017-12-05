Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"

  config.vm.provider :virtualbox do |v|
    v.memory = 2048
    v.linked_clone = true
  end

  config.vm.define "dev" do |dev|
    dev.vm.hostname = "development"
    dev.vm.network :private_network, ip: "192.168.100.3"
    dev.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh"
    dev.vm.network :forwarded_port, guest: 80, host: 8080, id: "localhost"

    (8001..8005).each do |i|
      dev.vm.network :forwarded_port, guest: "#{i}", host: "#{i}", host_ip: "127.0.0.1", auto_correct: false
    end

    dev.vm.synced_folder "/var/www", "/var/www",
    owner: "vagrant",
    group: "www-data"

  end
end

