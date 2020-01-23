# KeeWeb official docker container
# https://keeweb.info
# (C) Antelle 2017, MIT license https://github.com/keeweb/keeweb
# Based on nginx-ssl-secure https://github.com/MarvAmBass/docker-nginx-ssl-secure/

# Building locally:
# docker build -t keeweb .
# docker run --name keeweb -d -p 443:443 -p 80:80 -e 'DH_SIZE=512' -v $EXT_DIR:/etc/nginx/external/ keeweb

# Using pre-built image from dockerhub:
# If you have SSL certs, put your dh.pem, cert.pem, key.pem to /etc/nginx/external/ and run with:
# docker run --name keeweb -d -p 443:443 -p 80:80 -v $EXT_DIR:/etc/nginx/external/ antelle/keeweb
# Or, to generate self-signed cert, run:
# docker run --name keeweb -d -p 443:443 -p 80:80 -e 'DH_SIZE=512' antelle/keeweb

FROM armhfbuild/nginx
LABEL architecture="ARMv7"
MAINTAINER Azman0101 "azman0101@gmail.com"

ENV QEMU_EXECVE 1

COPY qemu/resin-xbuild qemu/qemu-arm-static /usr/bin/

RUN [ "qemu-arm-static", "/bin/sh", "-c", "ln -s resin-xbuild /usr/bin/cross-build-start; ln -s resin-xbuild /usr/bin/cross-build-end; mv /bin/sh /bin/sh.real; ln -s /bin/sh.real /bin/sh" ]

RUN [ "cross-build-start" ]
# install
RUN apt-get -y update && apt-get -y install openssl wget unzip && rm -rf /var/lib/apt/lists/*

# setup nginx
RUN rm -rf /etc/nginx/conf.d/*; \
    mkdir -p /etc/nginx/external

RUN sed -i 's/access_log.*/access_log \/dev\/stdout;/g' /etc/nginx/nginx.conf; \
    sed -i 's/error_log.*/error_log \/dev\/stdout info;/g' /etc/nginx/nginx.conf; \
    sed -i 's/^pid/daemon off;\npid/g' /etc/nginx/nginx.conf

ADD keeweb.conf /etc/nginx/conf.d/keeweb.conf

ADD entrypoint.sh /opt/entrypoint.sh
RUN chmod a+x /opt/entrypoint.sh

# clone keeweb
RUN wget https://github.com/keeweb/keeweb/archive/gh-pages.zip; \
    unzip gh-pages.zip; \
    rm gh-pages.zip; \
    mv keeweb-gh-pages keeweb; \
    rm keeweb/CNAME

# clone keeweb plugins
RUN wget https://github.com/keeweb/keeweb-plugins/archive/master.zip; \
    unzip master.zip; \
    rm master.zip; \
    mv keeweb-plugins-master/docs keeweb/plugins; \
    rm -rf keeweb-plugins-master \
    rm keeweb/plugins/CNAME

RUN [ "cross-build-end" ] 

ENTRYPOINT [ "/usr/bin/qemu-arm-static", "/usr/bin/env", "QEMU_EXECVE=1" ]

#ENTRYPOINT ["/opt/entrypoint.sh"]
CMD ["nginx"]

EXPOSE 443
EXPOSE 80
