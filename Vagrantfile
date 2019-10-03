# -*- mode: ruby -*-
# vi: set ft=ruby :

aws_cfg = (JSON.parse(File.read("scripts/aws.json")))

Vagrant.configure("2") do |config|
  config.vm.box = "dummy"

  config.vm.provider :aws do |aws, override|
    aws.region = "us-east-1"
    
    override.nfs.functional = false
    override.vm.allowed_synced_folder_types = :rsync

    aws.keypair_name = "cosc349"

    override.ssh.private_key_path = "~/.ssh/cosc349.pem"

    aws.instance_type = "t2.micro"

    aws.security_groups = ["sg-02433f243499ff78b"]

    aws.availability_zone = "us-east-1a"
    aws.subnet_id = "subnet-f57f2c92"

    aws.ami = "ami-04763b3055de4860b"

    override.ssh.username = "ubuntu"
  end

   config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y apache2
   SHELL
end
