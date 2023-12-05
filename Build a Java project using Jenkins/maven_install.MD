#### Install Maven on Jenkins

     # Creating maven directory under /opt
     mkdir /opt/maven
     cd /opt/maven
     # downloading maven version 3.6.0
     wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
     tar -xvzf apache-maven-3.9.6-bin.tar.gz
     ```
	
Setup M2_HOME and M2 paths in .bash_profile of the user and add these to the path variable
   
   vi ~/.bash_profile
    export JAVA_HOME=/usr
    export M2_HOME=/opt/maven/apache-maven-3.9.6
    export M2=$M2_HOME/bin
    export PATH=$PATH:$M2_HOME:$M2:$JAVA_HOME/bin:$HOME/.local/bin:$HOME/bin

source ~/.bash_profile

 mvn --version


### Setup maven on Jenkins console
1. Install maven plugin without restart  
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Integration`

2. Configure maven path
  - `Manage Jenkins` > `Global Tool Configuration` > `Maven`

### Build Java project on Jenkins console