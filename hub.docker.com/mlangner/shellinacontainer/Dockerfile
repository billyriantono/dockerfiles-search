FROM        alpine:3.4

COPY        build-on-alpine.patch /build-on-alpine.patch
COPY        cpanm-*.pl /usr/local/bin/cpanm

            # install build tools + other required apks
RUN         apk --update add \
                alpine-sdk autoconf automake libtool wget \
                wget perl socat apache2-utils nginx openssl \

            # build shellinabox
            && git clone https://github.com/shellinabox/shellinabox.git /shellinabox \
            && cd /shellinabox \
            && git apply /build-on-alpine.patch \
            && autoreconf -i \
            && ./configure \
            && make \
            && make install \
            && strip /usr/local/bin/shellinaboxd \

            # install docker
            && wget -qO - --no-check-certificate https://get.docker.com/builds/Linux/x86_64/docker-1.10.3.tgz \
               | tar xzf - -C / \
            && strip /usr/local/bin/docker \

            # install Mojolicious
            && cpanm -n Mojolicious \
            && rm -rf /root/.cpanm \

            # cleanup build tools
            && apk del alpine-sdk autoconf automake libtool wget \
            && rm -rf /var/cache/apk/* /shellinabox /etc/ssl/certs/* \
            && find /usr/share/perl5 -name *.pod -delete

COPY        nginx.conf /etc/nginx/nginx.conf
COPY        entrypoint.sh /
COPY        src/shellinacontainer /home/src/

WORKDIR     /home/

ENTRYPOINT  [ "/entrypoint.sh" ]
