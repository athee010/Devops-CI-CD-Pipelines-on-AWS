# Tomcat installation on EC2 instance

   # Install java11 
   # Create tomcat directory
   cd /opt
   wget http://mirrors.fibergrid.in/apache/tomcat/tomcat-8/v8.5.35/bin/apache-tomcat-9.0.83 tar.gz
   tar -xvzf /opt/apache-tomcat-9.0.83.tar.gz
   
give executing permissions to startup.sh and shutdown.sh which are under bin. 
   
   chmod +x /opt/apache-tomcat-9.0.83/bin/startup.sh 
   chmod +x /opt/apache-tomcat-9.0.83/bin/shutdown.sh
   

create link files for tomcat startup.sh and shutdown.sh 
   
   ln -s /opt/tomcat/bin/startup.sh /usr/local/bin/tomcatup
   ln -s /opt/tomcat/bin/shutdown.sh /usr/local/bin/tomcatdown
   tomcatup
   
tomcat application doesnt allow to login from browser. changing a default parameter in context.xml does address this issue
   
   #search for context.xml
   find / -name context.xml
   
comment (<!-- & -->) `Value ClassName` 
   /opt/tomcat/webapps/host-manager/META-INF/context.xml
   /opt/tomcat/webapps/manager/META-INF/context.xml
   
   

Update users information in the tomcat-users.xml file

cd bin/conf/
vi tomcat-users.xml file
   
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="deployer" roles="manager-script"/>
	<user username="tomcat" password="s3cret" roles="manager-gui"/>
   

Restart serivce and try to login to tomcat application from the browser. 