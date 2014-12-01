ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

DOCKER_HOST_NAME = "dockerhost"
BASE_NAME = "redis-cluster"
IMAGE_NAME = "#{BASE_NAME}-image"

#$script = <<SCRIPT
#cd /src/vertx
#git clone https://github.com/vert-x/vertx-examples.git
#SCRIPT

Vagrant.configure("2") do |config|

  #config.vm.provision "shell", inline: $script

  config.vm.define "#{IMAGE_NAME}" do |a|
    a.vm.provider "docker" do |d|
       
      #d.image = "#{IMAGE_NAME}:latest"
      d.build_dir = "."
       
      d.build_args = ["-t=#{IMAGE_NAME}"]
      d.ports = ["8080:8080"]
      d.name = "#{BASE_NAME}"
      d.remains_running = true
      #d.has_ssh = true
      d.cmd = [ "vertx", "run", "vertx-examples/src/raw/java/httphelloworld/HelloWorldServer.java" ]
      #d.volumes = ["/src/vertx/:/usr/local/src"]
       
      d.vagrant_machine = "#{DOCKER_HOST_NAME}"
      d.vagrant_vagrantfile = "./docker/Vagrantfile"
    end
  end
  #config.ssh.username = "root"
  #config.ssh.private_key_path =  "~/.ssh/id_rsa"
end
