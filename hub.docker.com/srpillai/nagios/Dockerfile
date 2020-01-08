FROM centos:7
MAINTAINER Sujith R Pillai<s.r.pillai@in.ibm.com>
# The installation reference : https://support.nagios.com/kb/article/nagios-core-installing-nagios-core-from-source-96.html#CentOS
# Map the following for custom configuration : <Your custom nagios.cfg file>:/usr/local/nagios/etc/nagios.cfg 
# Map the following for custom logging file  : <Your custom nagios.log file>:/usr/local/nagios/var/logs/nagios.log
# Map the following ENV for custom Nagios Admin user (default nagiosadmin) : NAGIOSADMIN=<Your custom Admin user>
# Map the following ENV for custom Nagios Admin pass (default admin) : NAGIOSPASS=<Your Custom Admin password>
ENV NAGIOSADMIN nagiosadmin
ENV NAGIOSPASS admin
RUN yum update ; \
    yum install -y gcc glibc glibc-common wget unzip httpd php gd gd-devel perl postfix make ; \
    yum clean all
RUN cd /tmp ; \
    wget -O nagioscore.tar.gz https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.4.1.tar.gz ; \
    tar xzf nagioscore.tar.gz ; \
    cd /tmp/nagioscore-nagios-4.4.1/ ; \
    ./configure ; \
    make all ; \
    make install-groups-users ; \
    usermod -a -G nagios apache ; \
    make install ; \
    make install-commandmode ; \
    make install-config ; \ 
    make install-webconf ; \
    rm -rf /tmp/* 
RUN cd /tmp ; \
    wget http://nagios-plugins.org/download/nagios-plugins-2.1.2.tar.gz ; \
    tar xzf nagios-plugins-2.1.2.tar.gz ; \
    cd /tmp/nagios-plugins-2.1.2 ; \
    ./configure --with-nagios-user=nagios --with-nagios-group=nagios ; \
    make ; \
    make install ; \
    rm -rf /tmp/*
RUN htpasswd -b -c /usr/local/nagios/etc/htpasswd.users ${NAGIOSADMIN} ${NAGIOSPASS} 
EXPOSE 80
COPY entrypoint.sh /usr/local/bin/entrypoint.sh
CMD [ "/usr/local/bin/entrypoint.sh" ]
