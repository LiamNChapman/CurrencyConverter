# -*- mode: ruby -*-
# vi: set ft=ruby :

aws_config = (JSON.parse(File.read("ec2_cfg.json")))

Vagrant.configure("2") do |config|
  config.vm.box = "dummy"

  aws_config['ec2s'].each do |node|
    node_name = node[0]
    node_value = node[1]

    config.vm.define node_name do |config2|
      ec2_tags = node_value['tags']
      
      config2.vm.provider :aws do |ec2, override|
        ec2.access_key_id = aws_config['access_key_id']
        ec2.secret_access_key = aws_config['secret_access_key_id']
        ec2.session_token = aws_config['session_token']
        ec2.keypair_name = aws_config['key_pair']
        ec2.region = aws_config['region']
        ec2.availability_zone = aws_config['availability_zone']
        override.ssh.private_key_path = aws_config['ssh_private_key']
        ec2.subnet_id = aws_config['subnet_id']
        ec2.security_groups = aws_config['security_groups']
        ec2.ami = node_value['ami_id']
        ec2.instance_type = node_value['instance_type']
        ec2.tags = {'Name' => ec2_tags['Name']}
        override.ssh.username = "ubuntu"

        override.nfs.functional = false
        override.vm.allowed_synced_folder_types = :rsync
      end
    end
  end
  
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y apache2
   SHELL
end
        
#  config.vm.provider :aws do |aws, override|
#    aws.region = "us-east-1"
    
#    override.nfs.functional = false
#    override.vm.allowed_synced_folder_types = :rsync

#    aws.keypair_name = "cosc349"

#    override.ssh.private_key_path = "~/.ssh/cosc349.pem"

#    aws.instance_type = "t2.micro"
#
#    aws.security_groups = ["sg-02433f243499ff78b"]
#
#    aws.availability_zone = "us-east-1a"
#    aws.subnet_id = "subnet-f57f2c92"
#
#    aws.ami = "ami-04763b3055de4860b"
#
 #   override.ssh.username = "ubuntu"
 # end

 #  config.vm.provision "shell", inline: <<-SHELL
 #    apt-get update
 #    apt-get install -y apache2
#   SHELL
#end
