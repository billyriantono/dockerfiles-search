FROM ubuntu:trusty
MAINTAINER ASCDC <asdc.sinica@gmail.com>

ADD run.sh /run.sh
ADD jdk-6u25-linux-x64.bin /root/jdk-6u25-linux-x64.bin
ENV JAVA_HOME="/root/jdk1.6.0_25/"

RUN DEBIAN_FRONTEND=noninteractive && \
	chmod +x /*.sh && \
	apt-get update && \
	apt-get -y install software-properties-common python-software-properties wget && \
	locale-gen en_US.UTF-8 && \
	export LANG=en_US.UTF-8 && \
	cd root && \
	wget http://archive.apache.org/dist/tomcat/tomcat-4/v4.1.30/bin/jakarta-tomcat-4.1.30.tar.gz && \
	tar zxvf jakarta-tomcat-4.1.30.tar.gz && \
	mv jakarta-tomcat-4.1.30 tomcat-4.1.30 && \
	chmod +x jdk-6u25-linux-x64.bin && \
	echo | /root/jdk-6u25-linux-x64.bin	 && \
	cp /usr/share/zoneinfo/Asia/Taipei /etc/localtime
	
WORKDIR /root/tomcat-4.1.30
ENTRYPOINT ["/run.sh"]
