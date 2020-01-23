FROM debian:jessie
MAINTAINER Boro <docker@bo.ro>

RUN apt-get update
RUN apt-get install -y tar wget ed make g++ pkg-config libpam0g-dev libsasl2-dev \
	        autotools-dev libltdl-dev libnetfilter-conntrack-dev nettle-dev \
	        libgnutls28-dev libexpat1-dev libxml2-dev libcppunit-dev libkrb5-dev \
            comerr-dev libcap2-dev automake libssl-dev tree libtool-bin apache2-utils

ADD deps /tmp/
RUN dpkg -i /tmp/*.deb

ADD build.sh /tmp/
ADD squid-3.5.27 /tmp/squidsrc
RUN chmod 777 /tmp/build.sh /tmp/squidsrc/*

RUN cd /tmp/squidsrc && /tmp/build.sh

# Setup some other custom things
RUN mkdir -p /etc/squid/blank_errors/templates
ENV EDITOR nano

# Add custom configuration files
ADD custom/squid.conf		/etc/squid/squid.conf
ADD custom/squid_passwd		/etc/squid/squid_passwd
ADD custom/error_templates	/etc/squid/blank_errors/templates

ADD start.sh /start.sh
# Convert any CRLF line endings to LF
RUN sed -i 's/\r//' /start.sh

RUN chmod 777 /var/log/squid/ /start.sh

EXPOSE 3128

WORKDIR /
CMD ["/start.sh"]