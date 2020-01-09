FROM kudato/baseimage:latest
LABEL maintainer="Alexander Shevchenko <kudato@me.com>"

ENV NETATALK_VERSION 3.1.11
ADD . /

RUN apk --no-cache upgrade && \
    apk add --update libldap libgcrypt linux-pam
RUN apk --no-cache add dbus dbus-glib
RUN apk --no-cache add cracklib db libevent
RUN apk --no-cache add avahi file acl openssl

RUN apk add --no-cache --virtual .build-deps \
    build-base autoconf automake libtool libgcrypt-dev linux-pam-dev \
    cracklib-dev acl-dev db-dev dbus-dev libevent-dev curl && cd /tmp && \
    curl -o netatalk-${NETATALK_VERSION}.tar.gz -L https://downloads.sourceforge.net/project/netatalk/netatalk/${NETATALK_VERSION}/netatalk-${NETATALK_VERSION}.tar.gz && \
    tar xvf netatalk-${NETATALK_VERSION}.tar.gz && \
    cd netatalk-${NETATALK_VERSION} && \
    CFLAGS="-Wno-unused-result -O2" ./configure \
      --prefix=/usr \
      --localstatedir=/var/state \
      --sysconfdir=/etc \
      --with-dbus-sysconf-dir=/etc/dbus-1/system.d/ \
      --with-init-style=debian-sysv \
      --sbindir=/usr/bin \
      --enable-quota \
      --with-tdb \
      --enable-silent-rules \
      --with-cracklib \
      --with-cnid-cdb-backend \
      --enable-pgp-uam \
      --with-acls && \
    make && \
    make install && \
    cd /tmp && rm -rf netatalk-${NETATALK_VERSION} netatalk-${NETATALK_VERSION}.tar.gz && \
    apk del .build-deps && rm -rf /tmp/* /var/tmp/* /var/cache/apk/* /var/cache/distfiles/* \
    /etc/avahi/services/* && mv /afpd.service /etc/avahi/services/afpd.service && \
    echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' > /etc/nsswitch.conf


ENV SPOTLIGHT_ENABLE True
ENV MODEL Xserve
# ENV TM_SIZE 


ENV DBUS_CMD dbus-daemon --system --nofork
ENV DBUS_NICE 0

ENV AVAHI_CMD avahi-daemon --no-chroot
ENV AVAHI_NICE 10

ENV AFPD_CMD netatalk -F /afp.conf -d
ENV AFPD_NICE 0

CMD [ "dbus", "avahi", "afpd" ]
