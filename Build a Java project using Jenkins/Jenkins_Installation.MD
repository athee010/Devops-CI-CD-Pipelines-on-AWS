## Install Jenkins

   sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
  sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
   amazon-linux-extras install epel 
   amazon-linux-extras install java-openjdk11  
   yum install jenkins

   service jenkins start
   service jenkins status

   cat /var/lib/jenkins/secrets/initialAdminPassword`