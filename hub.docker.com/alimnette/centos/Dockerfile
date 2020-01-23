FROM centos:centos6
MAINTAINER Alimnette

RUN yum install -y git curl wget tar

# PhpMyFaq requires PHP 5.4.4+
# Current in RHEL is PHP 5.3
# Install PHP5.4 from IUS (https://iuscommunity.org)
RUN cd /tmp; wget http://dl.iuscommunity.org/pub/ius/stable/CentOS/6/x86_64/ius-release-1.0-13.ius.centos6.noarch.rpm && yum install -y /tmp/ius-release-1.0-13.ius.centos6.noarch.rpm
RUN yum install -y php php-mysql php-gd php-xml

# Node from yum has dependency errors, so install Node from a tarball.
RUN cd /tmp/; wget http://nodejs.org/dist/v0.10.32/node-v0.10.32-linux-x64.tar.gz
# Per README.md in node-v0.10.31-linux-x64.tar.gz
RUN cd /usr/local && tar --strip-components 1 -xzf /tmp/node-v0.10.32-linux-x64.tar.gz

# http://forum.phpmyfaq.de/viewtopic.php?f=3&t=16624&sid=155675baaf712909037d7ecdb8aafcc0
RUN git clone git://github.com/thorsten/phpMyFAQ.git && cd phpMyFAQ && git checkout 2.8
RUN cd phpMyFAQ; curl -s https://getcomposer.org/installer | php && php composer.phar install
# Run with --unsafe-perm as we're building in a Docker container as root.
RUN cd phpMyFAQ; /usr/local/bin/npm install --unsafe-perm
RUN cd phpMyFAQ; grunt
