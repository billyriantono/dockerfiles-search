FROM land007/centos:7.5.1804
MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN yum update -y \
	&& yum install -y gcc-c++ gcc glibc-headers make openssl-devel pkg-config \
	&& yum clean all


#latest
#docker stop centos ; docker rm centos ; docker run -it --privileged --name centos land007/centos:latest
#7.5.1804
#docker stop centos ; docker rm centos ; docker run -it --privileged --name centos land007/centos:7.5.1804
