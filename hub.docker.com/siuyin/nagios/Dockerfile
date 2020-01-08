FROM phusion/baseimage:0.9.16
#FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install nagios3 nagios3-common nagios-plugin* nagios-nrpe* swaks postfix libsasl2-modules -y 
RUN postconf -e mynetworks="0.0.0.0/0"
RUN usermod -a -G nagios www-data
RUN htpasswd -b -c /etc/nagios3/htpasswd.users nagiosadmin insecure

# set environment so that vim and less work properly
ENV HOME=/root
ENV TERM=xterm
ENV ROOT_EMAIL=someone@example.com

RUN mkdir -p /etc/service/apache2
ADD run/apache2 /etc/service/apache2/run

RUN mkdir -p /etc/service/nagios3
ADD run/nagios3 /etc/service/nagios3/run
RUN dpkg-statoverride --update --add nagios www-data 2710 /var/lib/nagios3/rw; dpkg-statoverride --update --add nagios nagios 751 /var/lib/nagios3

RUN mkdir -p /etc/my_init.d
ADD rc/postfix.sh /etc/my_init.d/postfix.sh

EXPOSE 25 80

CMD ["/sbin/my_init"]

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

