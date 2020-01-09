FROM ubuntu:16.04

# Set HOME to suppress warnings
ENV  HOME /root

# For debconf not to complain
ENV  DEBIAN_FRONTEND noninteractive

# Ensure that all packages are latest and use AWS EU mirror
ADD  /root/etc/apt/sources.list /etc/apt/sources.list
RUN  echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup && \
     apt-get update -y && \
     apt-get install -y daemontools && \
     apt-get install -y curl openssl && \
     apt-get clean && apt-get autoremove && \
     rm -rf /var/lib/cache/* /var/lib/log/* /tmp/* /var/tmp/*

ADD  /root /
RUN  chmod a+x /usr/local/sbin/*

#RUN  chmod a+x /etc/services/*/run

CMD  /usr/bin/svscan /etc/services

