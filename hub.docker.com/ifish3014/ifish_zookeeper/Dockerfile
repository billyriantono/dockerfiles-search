FROM centos:centos7

MAINTAINER happylv lvhuanle12@126.com

# 更新和安装必要软件
RUN yum update -y && yum install -y wget

# 安装jdk8
RUN  echo "Install Java8"
RUN wget https://cloud-file-1256986650.cos.ap-beijing.myqcloud.com/jdk-8u202-linux-x64.tar.gz
RUN tar -zxvf jdk-8u202-linux-x64.tar.gz
RUN mv jdk1.8.0_202 /opt/jdk
RUN rm -rf jdk-8u202-linux-x64.tar.gz

# 安装zookeeper
RUN echo "Install zookeeper"
RUN wget https://cloud-file-1256986650.cos.ap-beijing.myqcloud.com/apache-zookeeper-3.5.5-bin.tar.gz
RUN tar -zxvf apache-zookeeper-3.5.5-bin.tar.gz
RUN mv apache-zookeeper-3.5.5-bin /opt/zookeeper
RUN mkdir /opt/zookeeper/data
ADD zoo.cfg /opt/zookeeper/conf/
RUN rm -rf apache-zookeeper-3.5.5-bin.tar.gz

# 配置路径
RUN echo "Config PATH"
ADD mypath.sh /etc/profile.d/
# RUN source /etc/profile

# 设置端口
EXPOSE 2181

# 启动zookeeper
CMD ["/opt/zookeeper/bin/zkServer.sh", "start"]
