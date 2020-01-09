FROM centos:latest
MAINTAINER tantan

ARG ASTERISK_VERSION
ENV ASTERISK_VERSION ${ASTERISK_VERSION:-asterisk-15-current}


RUN yum clean metadata \
  && yum -y update \
  && yum install epel-release -y \
  && yum install -y \
    @"Development Tools" \
    gnupg2 \
    libffi \
    libffi-devel \
    rsync \
    ruby \
    ruby-devel \
    rubygems \
    wget \
    curl \
    && gem install --no-ri --no-rdoc fpm \
	&& cd /tmp && wget http://downloads.asterisk.org/pub/telephony/asterisk/${ASTERISK_VERSION}.tar.gz \
  && tar zvxf ${ASTERISK_VERSION}.tar.gz \
  && rm ${ASTERISK_VERSION}.tar.gz \
  && cd /tmp/asterisk-* \
  && ./contrib/scripts/install_prereq install \
  && ./contrib/scripts/install_prereq install-unpackaged \
  && ./configure \
  && cd menuselect \
  && make menuselect \
  && cd .. \
  && make menuselect-tree \
  && menuselect/menuselect --check-deps menuselect.makeopts \
  && sed -i -e 's/MENUSELECT_MOH=.*$/MENUSELECT_MOH=/' menuselect.makeopts \
  && sed -i -e 's/MENUSELECT_CORE_SOUNDS=.*$/MENUSELECT_CORE_SOUNDS=/' menuselect.makeopts \
  && make all install DESTDIR=/build/out \
  && make samples DESTDIR=/build/out \
	&& yum clean all \
	&& rm -rf /var/lib/apt/lists/* \
	&& tar czvf /tmp/contrib.tgz ./contrib
	

RUN fpm -t rpm -s dir \
    -n ${ASTERISK_VERSION} \
    --version 0.0.0 \
    -C /build/out var etc usr

FROM centos:latest

ENV ASTERISK_VERSION ${ASTERISK_VERSION:-asterisk-15-current}
COPY --from=0 ${ASTERISK_VERSION}-0.0.0-1.x86_64.rpm .
COPY --from=0 /tmp/contrib.tgz .

RUN yum install epel-release -y && \
  yum install -y \
  libedit libxslt jansson \
  pjproject \
  openssl \
  libxml2 \
  unixODBC \
  libcurl \
  libogg \
  libvorbis \
  speex \
  spandsp \
  freetds \
  net-snmp \
  iksemel \
  corosynclib \
  newt \
  lua \
  sqlite \
  freetds \
  radiusclient-ng \
  postgresql \
  neon \
  libical \
  openldap \
  sqlite2 \
  mysql \
  bluez \
  gsm \
  libuuid \
  libsrtp \
  php php-cli php-common php-dba php-gd php-mbstring php-odbc php-pdo php-pgsql \
	&& tar zvxf contrib.tgz \
	&& ./contrib/scripts/install_prereq install \
 	&& ./contrib/scripts/install_prereq install-unpackaged \
	&& rm ./contrib.tgz \
  &&  yum install -y ${ASTERISK_VERSION}-0.0.0-1.x86_64.rpm \
  && yum clean all \
  && yum autoremove -y \
  && rm -rf /var/lib/apt/lists/* \
  && /sbin/ldconfig 

ENTRYPOINT ["/usr/sbin/asterisk"]
CMD ["-c", "-vvvv", "-g"]
