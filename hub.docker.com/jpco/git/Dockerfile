FROM codingwell/rpi-raspbian-qemu

MAINTAINER  J.P.C. Oudeman

RUN [ "cross-build-start" ]
COPY assets/bin/*.sh /usr/local/bin/

RUN echo "deb http://ppa.launchpad.net/git-core/ppa/ubuntu precise main" > /etc/apt/sources.list.d/git.list && \
 apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E1DF1F24 && \
 apt-get update && \
 apt-get install -y git openssh-client && \
 rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
 mkdir -p /var/www/.ssh && \
 mkdir /var/workspace && \
 chown www-data: /var/www/.ssh && \
 chown www-data: /var/workspace && \
 chmod a+x /usr/local/bin/*.sh

RUN [ "cross-build-end" ]  

# workspace to do work 
VOLUME /var/workspace
WORKDIR /var/workspace

USER www-data

CMD ["bash"]
