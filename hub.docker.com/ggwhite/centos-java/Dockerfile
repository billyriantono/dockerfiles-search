FROM centos:7

MAINTAINER ggwhite <ggw.chang@gmail.com>

### Actions
# 更新 yum
# 安裝 wget
# 下載java jre 8，要加header，才能成功下載
# 安裝 java rpm
# 移除 rpm檔
# 清空 yum 資源

RUN yum update -y && \ 
	yum install -y wget && \ 
	wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.rpm && \ 
	yum localinstall -y /jdk-8u111-linux-x64.rpm && \ 
	rm -f /jdk-8u111-linux-x64.rpm && \ 
	yum clean all 

# Set environment variables.
ENV HOME /root
ENV JAVA_HOME /usr/java/default/

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["/bin/bash"]