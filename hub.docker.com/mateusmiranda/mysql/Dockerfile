# MySql Percona Image
#
# VERSION               0.0.1
 
FROM mateusmiranda/ubuntu
 
MAINTAINER Mateus Miranda <mateusmiranda@gmail.com>
 
# Install Ref: http://www.percona.com/doc/percona-server/5.6/installation/apt_repo.html
RUN apt-key adv --keyserver keys.gnupg.net --recv-keys 1C4CBDCDCD2EFD2A && \
        echo "deb http://repo.percona.com/apt trusty main" >> /etc/apt/sources.list && \
        echo "deb-src http://repo.percona.com/apt trusty main" >> /etc/apt/sources.list
 
RUN apt-get update && \
        apt-get -y install percona-server-server-5.6 percona-server-client-5.6 percona-toolkit
 
# Add dump file inside the image
#ADD developer_dump.sql.bz2 /tmp/developer_dump.sql.bz2
 
# Copy external mysql configuration
COPY custom.cnf /etc/mysql/conf.d/custom.cnf
 
# Set Server accessible from outside the container - Could be set in mobly.cnf, but this is not optional, it's a RULE!
RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf

ADD ./startdb.sh /opt/startdb.sh
RUN chmod +x /opt/startdb.sh

EXPOSE 3306
 
CMD ["/bin/bash", "/opt/startdb.sh"]
