FROM    jsmigel/centos-epel:centos6
MAINTAINER jsmigel@users.noreply.github.com

RUN yum -y install ngircd
RUN yum -y update

ADD ngircd.conf /etc/ngircd.conf

EXPOSE 6667

ENTRYPOINT [ "/usr/sbin/ngircd", "-n" ]
