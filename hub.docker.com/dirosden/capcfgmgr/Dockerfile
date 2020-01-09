FROM gliderlabs/alpine

LABEL name="Alpine OS Base Image"
LABEL vendor="AlpineOS"
LABEL license=GPLv2

ENV REFRESHED_AT 2016-12-15

# - Install basic packages (e.g. python-setuptools is required to have python's easy_install)
# - Install yum-utils so we have yum-config-manager tool available
# - Install jq, small library for handling JSON files/api from CLI
# - Install supervisord (via python's easy_install - as it has the newest 3.x version)

RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.4/community" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/v3.4/main" >> /etc/apk/repositories      && \
    echo "http://alpine.gliderlabs.com/alpine/edge/community" >> /etc/apk/repositories  && \
    echo "http://alpine.gliderlabs.com/alpine/edge/testing" >> /etc/apk/repositories    && \
    echo "http://alpine.gliderlabs.com/alpine/edge/main" >> /etc/apk/repositories       && \
    
      # make some useful symlinks that are expected to exist
    if [[ ! -e /usr/bin/python ]];        then ln -sf /usr/bin/python2.7 /usr/bin/python; fi \
    && if [[ ! -e /usr/bin/python-config ]]; then ln -sf /usr/bin/python2.7-config /usr/bin/python-config; fi \
    && if [[ ! -e /usr/bin/idle ]];          then ln -sf /usr/bin/idle2.7 /usr/bin/idle; fi \
    && if [[ ! -e /usr/bin/pydoc ]];         then ln -sf /usr/bin/pydoc2.7 /usr/bin/pydoc; fi \
    && if [[ ! -e /usr/bin/easy_install ]]; then ln -sf /usr/bin/easy_install-2.7 /usr/bin/easy_install; fi 

    
RUN apk update && \
    apk add bash curl iproute2 py-setuptools which jq supervisor ca-certificates && \
    
    # Salt and prerequisites
    apk add salt-master  \
            salt-minion  \
            salt-ssh     \
            py-inotify   \
            virt-what && \

    # Additional tools
    apk add net-tools nmap git && \
        
    easy_install dirsync

# Moving Runtime Configuration for Main Components - Supervisor and Salt Minion 
ADD config   /config
ADD etc	     /etc 
ADD srv      /srv

RUN mkdir -p /var/log/supervisor

# Expose volumes
VOLUME ["/var/log/supervisor"]

# Expose ports for salt
EXPOSE 4505
EXPOSE 4506

RUN ["chmod", "+x", "/config/bootstrap.sh"]
RUN ["chmod", "+x", "/config/init/configureenv.sh"]
RUN ["chmod", "+x", "/config/init/setupminion.sh"]

#Running the Start Script
CMD ["/config/bootstrap.sh"]
