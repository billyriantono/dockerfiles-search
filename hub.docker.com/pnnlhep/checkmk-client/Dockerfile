FROM pnnlhep/osg-base
MAINTAINER James Czebotar "James.Czebotar@pnnl.gov"

ADD ./start.sh /etc/start.sh
RUN \
  yum install -y crontabs cronie-anacron check-mk-agent && \
  chmod +x /etc/start.sh && \
  sed -i 's/^\(.*pam_loginuid.so\)$/#\1/' /etc/pam.d/crond && \
  echo "*/4 * * * * export PATH=\$PATH:/usr/sbin; /usr/bin/check_mk_agent > /dev/shm/\$HOSTNAME ; curl --insecure -X POST -F \"data=@/dev/shm/\$HOSTNAME\" @URL@ > /dev/null 2>&1" >> /etc/crontab.template 

CMD ["/etc/start.sh"]
