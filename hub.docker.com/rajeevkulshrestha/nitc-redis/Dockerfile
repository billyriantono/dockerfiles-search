FROM centos:7
MAINTAINER Rajeev Kulshrestha rajeev.kulshrestha@ocio.usda.gov
ENV PATH /usr/local/src/vendor/bin/:/usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Fix command line compile issue with bundler.
ENV LC_ALL en_US.utf8

# Install and enable repositories
RUN yum -y update && \
    yum -y install epel-release && \
    rpm -Uvh https://centos7.iuscommunity.org/ius-release.rpm && \
    yum -y update

RUN groupadd -r redis && useradd -r -g redis redis

RUN yum install redis sudo -y && \
    yum clean all

RUN sed 's/daemonize yes/daemonize no/' -i /etc/redis.conf && \
    sed 's/bind 127.0.0.1/bind 0.0.0.0/' -i /etc/redis.conf && \
    sed '/^logfile/d' -i /etc/redis.conf && \
    sed -i 's/Defaults    requiretty/#Defaults    requiretty/g' /etc/sudoers


ADD start /start
RUN chmod 755 /start

ENV MAXCLIENTS 2000
EXPOSE 6379
VOLUME ["/var/lib/redis"]
CMD ["/start"]