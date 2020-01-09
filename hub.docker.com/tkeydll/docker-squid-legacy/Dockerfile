FROM centos:6

WORKDIR /root

# Install squid.
RUN yum install -y wget \
 && wget http://mirror.centos.org/centos/6/os/x86_64/Packages/squid-3.1.23-24.el6.x86_64.rpm \
 && yum localinstall -y squid-3.1.23-24.el6.x86_64.rpm \
 && rm /etc/squid/squid.conf

COPY squid.conf /etc/squid/squid.conf
COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh

EXPOSE 3128/tcp
ENTRYPOINT ["/sbin/entrypoint.sh"]
