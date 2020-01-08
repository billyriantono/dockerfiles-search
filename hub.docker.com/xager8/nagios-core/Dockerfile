FROM centos:7

RUN yum install -y gcc gd gd-devel iputils-ping make openssl openssl-devel perl php unzip wget
RUN useradd nagios && usermod -a -G nagios apache

RUN wget -q https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.5.tar.gz && \
    tar xf nagios-4.4.5.tar.gz && \
    cd nagios-4.4.5 && \
    ./configure && \
    make all && \
    make install && \
    make install-commandmode && \
    make install-config && \
    make install-webconf && \
    sed -i 's|main.php|cgi-bin/tac.cgi|' /usr/local/nagios/share/index.php && \
    htpasswd -b -c /usr/local/nagios/etc/htpasswd.users nagiosadmin nagiosadmin

RUN wget -q https://nagios-plugins.org/download/nagios-plugins-2.2.1.tar.gz && \
    tar xf nagios-plugins-2.2.1.tar.gz && \
    cd nagios-plugins-2.2.1 && \
    ./configure && \
    make install

RUN wget -q https://github.com/NagiosEnterprises/nrpe/releases/download/nrpe-3.2.1/nrpe-3.2.1.tar.gz && \
    tar xf nrpe-3.2.1.tar.gz && \
    cd nrpe-3.2.1 && \
    ./configure && \
    make check_nrpe && \
    make install-plugin

COPY run /run.sh
EXPOSE 80/tcp
CMD ["/run.sh"]
