FROM oraclelinux:7-slim
MAINTAINER Erik LaBianca <erik@7thsense.io>
RUN yum -y update && yum clean all
ADD bootstrap.sh /root/bootstrap.sh
RUN /root/bootstrap.sh
