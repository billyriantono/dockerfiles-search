FROM reisen/debian-arm-qemu

RUN [ "cross-build-start" ]

RUN apt-get update \
 && apt-get -y dist-upgrade \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y curl wget make gcc g++ gosu 

RUN curl -sL https://deb.nodesource.com/setup_11.x | bash - \
 && apt-get install -y nodejs

RUN npm install -g --unsafe-perm node-red

RUN apt-get -y remove curl wget make gcc g++ \
 && apt-get -y autoremove \
 && apt-get -y clean \
 && rm -rf /var/lib/apt/lists/*

# Verify if gosu is working
RUN gosu nobody true

COPY entrypoint.sh /usr/sbin/

RUN chmod 755 /usr/sbin/entrypoint.sh

RUN [ "cross-build-end"]

CMD ["/usr/sbin/entrypoint.sh"]
