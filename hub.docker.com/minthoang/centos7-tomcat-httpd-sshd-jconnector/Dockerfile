FROM centos:latest

WORKDIR /opt

RUN yum update -y
    
	#install and config sshd
RUN yum install openssh-server -y && \
	ssh-keygen -A && \
	echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
    
	
	# install java
RUN yum install java-1.8.0-openjdk-devel -y && \
    
	# install httpd
	yum install httpd -y && \
	
	# package install j-connector
    yum install httpd-devel apr apr-devel apr-util apr-util-devel gcc gcc-c++ make autoconf libtool -y

COPY conf /etc/httpd/conf
COPY conf.modules.d /etc/httpd/conf.modules.d
COPY conf.d /etc/httpd/conf.d
COPY mod_jk.so /etc/httpd/modules
    
	# install wget
RUN yum install wget -y &&\
    
	# dowload tomcat 9 and extract the file
        wget http://mirrors.viethosting.com/apache/tomcat/tomcat-9/v9.0.26/bin/apache-tomcat-9.0.26.tar.gz && \
	tar -zxvf apache-tomcat-9.0.26.tar.gz && \
	mv apache-tomcat-9.0.26 tomcat && \
	
	# dowload tomcat connector and extract the file
	wget http://mirror.downloadvn.com/apache/tomcat/tomcat-connectors/jk/tomcat-connectors-1.2.46-src.tar.gz && \
	tar -zxvf tomcat-connectors-1.2.46-src.tar.gz && \
	mv tomcat-connectors-1.2.46-src connector && \
	
	# delete source 
	rm -rf apache-tomcat-9.0.26.tar.gz tomcat-connectors-1.2.46-src.tar.gz 

    # environment variable
RUN	echo "export CATALINA_HOME="/opt/tomcat"" >> ~/.bashrc && \
    echo "export JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-1.el7_7.x86_64/jre/bin/java"" >> ~/.bashrc && \
	echo "export JRE_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-1.el7_7.x86_64"" >> ~/.bashrc && \
	source ~/.bashrc && \
    cd /opt/connector/native && \
	
	# install connector
	./configure --with-apxs=/usr/bin/apxs && \
    make
	
    # install and configure supervisord on centos 7 	
RUN yum install -y python-setuptools && \
    easy_install supervisor && \
    mkdir -p /var/log/supervisor && \
    mkdir -p /etc/supervisor/conf.d 

EXPOSE 8080 80 22
COPY supervisor.conf /etc/supervisor.conf
CMD ["supervisord", "-c", "/etc/supervisor.conf"]


	
	

