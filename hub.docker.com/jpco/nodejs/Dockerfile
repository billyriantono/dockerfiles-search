FROM codingwell/rpi-raspbian-qemu

MAINTAINER  J.P.C. Oudeman

##
# Might want to map the sourcefiles to /var/lib/node/app
##

COPY assets/bin/entrypoint.sh /usr/local/bin

# Install node
RUN [ "cross-build-start" ]
RUN apt-get update && \
 apt-get install -y apt-transport-https curl && \
 curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
 echo 'deb https://deb.nodesource.com/node_4.x jessie main' > /etc/apt/sources.list.d/nodesource.list && \
 apt-get update && \
 apt-get install -y nodejs && \
\
# prepare environment
 mkdir -p /var/lib/node/app /var/www && \
 chown www-data: /var/lib/node/app /var/www && \
 chmod +x /usr/local/bin/*.sh && \
 rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN [ "cross-build-end" ]

USER www-data

ENTRYPOINT ["entrypoint.sh"]
CMD ["npm", "start"]
ENV WORKDIR /var/lib/node/app
WORKDIR $WORKDIR