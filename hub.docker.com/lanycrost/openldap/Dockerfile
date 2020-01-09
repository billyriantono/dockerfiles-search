FROM lanycrost/alpine:3.8

LABEL maintainer="Khachatur Ashotyan (lanycrost)"
LABEL version="0.1"
LABEL description="OpenLDAP server w/TLS + replication support, S6 overlay, Fusion Directory schema's included."

ENV ADMIN_PASS=admin
ENV BACKEND=mdb
ENV BACKUP_CONFIG_CRON_PERIOD="0 4 * * *"
ENV BACKUP_DATA_CRON_PERIOD="0 4 * * *"
ENV BACKUP_TTL=15
ENV CONFIG_PASS=config
ENV DOMAIN=vtg.local
ENV ENABLE_READONLY_USER=false
ENV ENABLE_REPLICATION=false
ENV ENABLE_SMTP=FALSE
ENV ENABLE_TLS=true
ENV LOG_LEVEL=256
ENV OPENLDAP_VERSION=2.4.46
ENV ORGANIZATION="VTG Software"
ENV READONLY_USER_PASS=readonly
ENV READONLY_USER_USER=readonly
ENV REMOVE_CONFIG_AFTER_SETUP=false
ENV SCHEMA2LDIF_VERSION=1.3
ENV SCHEMA_TYPE=nis
ENV SSL_HELPER_PREFIX=ldap
ENV TLS_CA_CRT_FILENAME=ca.pem
ENV TLS_CIPHER_SUITE="ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESGCM:RSA+AES:-DHE-DSS:-RSA:!aNULL:!MD5:!DSS:!SHA"
ENV TLS_CRT_FILENAME=cert.pem
ENV TLS_ENFORCE=false
ENV TLS_KEY_FILENAME=key.pem
ENV TLS_VERIFY_CLIENT=try
ENV FUSIONDIRECTORY_VERSION=1.2.1

# Add OpenLDAP user and group
RUN set -x && \
  addgroup -g 389 ldap && \
  adduser -S -D -H -h /var/lib/openldap -s /sbin/nologin -G ldap -u 389 ldap

# Fetch Build Dependencies
RUN set -x && \
  apk update && \
  apk add -t .openldap-build-deps \
    autoconf \
    automake \
    build-base \
    cracklib-dev \
    cyrus-sasl-dev \
    db-dev \
    git \
    groff \
    libressl-dev \
    libtool \
    m4 \
    mosquitto-dev \
    unixodbc-dev \
    util-linux-dev

# Fetch Runtime Dependencies
RUN set -x && \
  apk update && \
  apk add -t .openldap-run-deps \
    cyrus-sasl \
    coreutils \
    cracklib \
    libressl \
    libltdl \
    libuuid \
    libintl \
    perl \
    sed \
    unixodbc

# Grab OpenLDAP Source, Alpine Patches and Check ppolicy module
RUN set -x && \
  mkdir -p /lanycrost/openldap/ && \
  curl -sSL ftp://ftp.openldap.org/pub/OpenLDAP/openldap-release/openldap-$OPENLDAP_VERSION.tgz | tar xvfz - --strip 1 -C /lanycrost/openldap/ && \
  git clone --depth 1 git://git.alpinelinux.org/aports.git /lanycrost/openldap/alpine && \
  mkdir -p contrib/slapd-modules/ppolicy-check-password && \
  git clone https://github.com/cedric-dufour/ppolicy-check-password /lanycrost/openldap/contrib/slapd-modules/ppolicy-check-password && \
  mkdir -p contrib/slapd-modules/ppm && \
  git clone https://github.com/ltb-project/ppm /lanycrost/openldap/contrib/slapd-modules/ppm && \
  cd /lanycrost/openldap/alpine && \
  git filter-branch --prune-empty --subdirectory-filter main/openldap HEAD && \
  rm -rf CVE-2017-9287.patch && \
  cd /lanycrost/openldap/ && \
  for patch in ./alpine/*.patch; do echo "** Applying $Patch"; patch -p1 < $patch; done

# Compile OpenLDAP
RUN set -x && \
  cd /lanycrost/openldap/ && \
  libtoolize --force && \
  aclocal && \
  autoconf && \
  ./configure \
    --build=$CBUILD \
    --host=$CHOST \
    --prefix=/usr \
    --libexecdir=/usr/lib \
    --sysconfdir=/etc \
    --mandir=/usr/share/man \
    --localstatedir=/var/run/openldap \
    --enable-slapd \
    --enable-crypt \
    --enable-modules \
    --enable-dynamic \
    --enable-bdb=mod \
    --enable-dnssrv=mod \
    --enable-hdb=mod \
    --enable-ldap=mod \
    --enable-mdb=mod \
    --enable-meta=mod \
    --enable-monitor=yes \
    --enable-null=mod \
    --enable-passwd=mod \
    --enable-spasswd \
    --enable-relay=mod \
    --enable-shell=mod \
    --enable-sock=mod \
    --enable-sql=mod \
    --enable-overlays=mod \
    --with-tls=openssl \
    --with-cyrus-sasl && \
    make DESTDIR="" install && \
    ## Build MQTT overlay.
    make DESTDIR="" prefix=/usr libexec=/usr/lib -C contrib/slapd-modules/mqtt install && \
    ## Build passwd pbkdf2.
    make DESTDIR="" prefix=/usr libexecdir=/usr/lib -C contrib/slapd-modules/passwd/pbkdf2 install && \
    ## Build ppolicy-check Module
    cd /lanycrost/openldap/ && \
    make prefix=/usr libexecdir=/usr/lib -C contrib/slapd-modules/ppolicy-check-password LDAP_INC_PATH=/lanycrost/openldap && \
    cp /lanycrost/openldap/contrib/slapd-modules/ppolicy-check-password/check_password.so /usr/lib/openldap && \
    ## Build Alternative PPM Module
    cd /lanycrost/openldap/ && \
    make prefix=/usr libexecdir=/usr/lib -C contrib/slapd-modules/ppm LDAP_INC_PATH=/lanycrost/openldap && \
    cp /lanycrost/openldap/contrib/slapd-modules/ppm/ppm.so /usr/lib/openldap

# OpenLDAP Setup
RUN set -x && \
  ln -s /usr/lib/slapd /usr/sbin && \
  mkdir -p /usr/share/doc/openldap && \
  mv /etc/openldap/*.default /usr/share/doc/openldap && \
  rm -rf /etc/openldap/* && \
  mkdir -p /etc/openldap/sasl2 && \
  echo "mech_list: plain external" > /etc/openldap/sasl2/slapd.conf && \
  mkdir -p /etc/openldap/schema && \
  cp -R /lanycrost/openldap/servers/slapd/schema/*.schema /etc/openldap/schema && \
  mkdir -p /run/openldap && \
  chown -R ldap:ldap /run/openldap

# SSL Helpers
RUN set -x && \
  curl -o /usr/sbin/cfssl -SL https://pkg.cfssl.org/R1.2/cfssl_linux-amd64 && \
  chmod 700 /usr/sbin/cfssl && \
  curl -o /usr/sbin/cfssljson -SL https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64 && \
  chmod 700 /usr/sbin/cfssljson

# Install Schema2LDIF
RUN set -x && \
  curl https://codeload.github.com/fusiondirectory/schema2ldif/tar.gz/${SCHEMA2LDIF_VERSION} | tar xvfz - --strip 1 -C /usr && \
  rm -rf /usr/Changelog && \
  rm -rf /usr/LICENSE

# Create Cracklib Dictionary
RUN set -x && \
  mkdir -p /usr/share/dict && \
  cd /usr/share/dict && \
  wget https://github.com/cracklib/cracklib/releases/download/cracklib-2.9.6/cracklib-words-2.9.6.gz && \
  create-cracklib-dict -o pw_dict cracklib-words-2.9.6.gz && \
  rm -rf cracklib-words-2.9.6.gz

# Install FusionDirectory
RUN mkdir -p /usr/src/fusiondirectory /usr/src/fusiondirectory-plugins/fusiondirectory-plugins && \
  curl https://codeload.github.com/fusiondirectory/fusiondirectory/tar.gz/fusiondirectory-${FUSIONDIRECTORY_VERSION} | tar xvfz - --strip 1 -C /usr/src/fusiondirectory && \
  curl https://codeload.github.com/fusiondirectory/fusiondirectory-plugins/tar.gz/fusiondirectory-${FUSIONDIRECTORY_VERSION} | tar xvfz - --strip 1 -C /usr/src/fusiondirectory-plugins

# Cleanup
RUN set -x && \
  apk del \
    .openldap-build-deps && \
  rm -rf /lanycrost \
  /var/cache/apk/* && \
  mkdir -p /etc/openldap/schema/fusiondirectory && \
  rm -rf /usr/src/fusiondirectory/contrib/openldap/rfc2307bis.schema && \
  cp /usr/src/fusiondirectory/contrib/bin/fusiondirectory-insert-schema /usr/sbin && \
  cp -R /usr/src/fusiondirectory/contrib/openldap/*.schema /etc/openldap/schema/fusiondirectory && \
  cp -R /usr/src/fusiondirectory-plugins/*/contrib/openldap/*.schema /etc/openldap/schema/fusiondirectory && \
  sed -i -e "s|/etc/ldap/schema|/etc/openldap/schema|g" /usr/sbin/fusiondirectory-insert-schema && \
  chmod +x /usr/sbin/fusiondirectory-insert-schema && \
  rm -rf /usr/src/*

# Add Assets
ADD install /

# S6 sctipts permissions
RUN set -x && \
  chmod -R u+x /etc/s6 && \
  chmod -R u+x /etc/cont-init.d

EXPOSE 389 636
