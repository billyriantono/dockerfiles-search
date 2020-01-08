# BASE IMAGE
FROM centos:latest

# YUM
RUN yum install --quiet --assumeyes \
    curl-devel \
    gcc \
    httpd \
    make \
    mysql \
    mysql-devel \
    php \
    php-bcmath \
    php-gd \
    php-mbstring \
    php-mysql \
    php-xml \
    vim \
    wget
	
# Get Software
RUN ["mkdir", "-p", "/source/zabbix"]
RUN ["wget", "--quiet", "-O", "/source/download", "http://sourceforge.net/projects/zabbix/files/latest/download"]

# Unpackage Software
WORKDIR /source
RUN ["tar", "-xzf", "download", "-C", "zabbix", "--strip-components", "1"]

# Configure Software
WORKDIR /source/zabbix
RUN ["sh", "configure", "--enable-server", "--enable-agent", "--with-mysql", "--with-libcurl"]

# Build software and move bins,configs
RUN ["make"]

ENTRYPOINT ["ls"]
CMD ["/source/zabbix/"]
