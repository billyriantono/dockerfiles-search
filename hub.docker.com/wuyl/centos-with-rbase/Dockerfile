#Dockerfile centos-rbase
# 选择一个已有的os镜像作为基础
FROM wuyl/centos-with-java:latest

# 镜像的作者
MAINTAINER wuyl

# 安装epel仓库
RUN yum install -y epel-release

# 安装openssh-server和sudo软件包，并且将sshd的UsePAM参数设置成no
RUN yum install -y R
