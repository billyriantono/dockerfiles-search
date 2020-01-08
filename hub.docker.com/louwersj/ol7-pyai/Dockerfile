FROM oraclelinux:7-slim

MAINTAINER Johan Louwers Capgemini version: 0.1


RUN rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm &&\
rpm -ivh https://rhel7.iuscommunity.org/ius-release.rpm &&\
yum -y groupinstall development &&\
yum -y install python36u python36u-pip python36u-devel &&\
yum clean all &&\
rm -rf /var/cache/yum/* &&\
rm -rf /var/tmp/*

# no real need for an EXPOSE at this moment in time 
#EXPOSE 80

# no real need for a CMD at this moment in time
#CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
