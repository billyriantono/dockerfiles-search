FROM fedora:29

RUN yum -y install nagios; yum clean all
RUN rm -rf /etc/nagios; install -m 775 -o root -g root -d /etc/nagios
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["sh", "/entrypoint.sh"]
