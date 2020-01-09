FROM centos:7

MAINTAINER Sandro Bastos de Oliveira>

RUN 	yum -y install epel-release
RUN	yum -y install firebird-superclassic
RUN 	yum -y remove epel-release
RUN	yum -y clean all

ADD ./aliases.conf /etc/firebird/aliases.conf

ADD ./firebird.conf /etc/firebird/firebird.conf

ADD ./fbtrace.conf /etc/firebird/fbtrace.conf

RUN ln -sf /dev/stdout /var/log/firebird/firebird.log

RUN chown firebird.firebird /var/lib/firebird/data/ -R

EXPOSE 3050
CMD "/usr/sbin/fbguard"
