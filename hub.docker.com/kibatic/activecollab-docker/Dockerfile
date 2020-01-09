FROM kibatic/symfony:7.1

RUN apt-get -qqq update && export DEBIAN_FRONTEND=noninteractive &&\
    apt-get install -qqq -y \
         openssl \
         php7.1-curl \
         php7.1-imap \
         php7.1-mysqli \
         php7.1-gd \
         php7.1-mbstring &&\
    # Cleanup apt
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /var/lib/php/sessions && chmod -R a+rw /var/lib/php/sessions

ADD rootfs /

