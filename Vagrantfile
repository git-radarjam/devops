BASE = <<-HEREDOC
##############################
# Docker
##############################
echo "Installing Docker"
yum install -y epel-release device-mapper-persistent-data lvm2
yum install -y docker
systemctl enable docker
systemctl start docker

##############################
#Docker Compose
##############################
echo "Installing Docker Compose"
yum install epel-release
yum install -y python-pip
pip install docker-compose
yum upgrade python
docker-compose version

##############################
# Tools
##############################
echo "Installs tools"
yum install -y wget
yum install -y net-tools
yum install -y git
yum install -y npm

##############################
# Jenkins
##############################
echo "Installs Jenkins"
wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
yum install -y jenkins
yum install -y java-1.8.0-openjdk.x86_64
systemctl enable jenkins
systemctl start jenkins
HEREDOC

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.network "forwarded_port", guest: 22, host: 50022
  config.vm.network "forwarded_port", guest: 80, host: 50080
  config.vm.network "forwarded_port", guest: 8080, host: 8888
  config.vm.network :forwarded_port, guest: 8124, host: 8124
  config.vm.provision "file", source: "./" , destination: "~/"
  config.vm.provision "shell", inline:BASE
end