FROM centos:7.6.1810

LABEL name="Centos 7.6.1810 + epel-release" \
    vendor="CentOS" \
    license="GPLv2" \
    maintainer="helion@mendanha.com.br" \
    build-date="20190226" 
	
RUN yum -y install epel-release \
	&& yum -y upgrade \
	&& yum -y update \
	&& yum clean all \
	&& rm /etc/localtime \
	&& ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime \
	&& date

WORKDIR /root
