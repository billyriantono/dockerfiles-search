FROM alpine:3.3

LABEL maintainer="Khachatur Ashotyan (lanycrost)"
LABEL version="3.3"
LABEL description="Improved version of Alpine. W/s6 overlay, zabbix agent, cron, bash, curl, less, vim."

# Set Defaults
ARG S6_OVERLAY_VERSION=v1.21.7.0
ARG MAJOR_VERSION=3.4
ARG ZBX_VERSION=${MAJOR_VERSION}.14
ARG ZBX_SOURCES=svn://svn.zabbix.com/tags/${ZBX_VERSION}/

ENV DEBUG_MODE=FALSE
ENV ENABLE_CRON=TRUE
ENV ENABLE_ZABBIX=FALSE

# Add Core Utils
RUN set -x && \
  apk --no-cache upgrade && \
  apk --no-cache add \
    bash \
    curl \
    grep \
    less \
    logrotate \
    tzdata \
    vim \
    && \
  rm -rf /var/cache/apk/* && \
  rm -rf /etc/logrotate.d/acpid && \
  cp -R /usr/share/zoneinfo/Asia/Yerevan /etc/localtime && \
  echo 'Asia/Yerevan' > /etc/timezone

# Zabbix Pre Installation steps
RUN set -x && \
  addgroup -g 10050 zabbix && \
  adduser -S -D -H -h /dev/null -s /sbin/nologin -G zabbix -u 10050 zabbix && \
  mkdir -p /etc/zabbix && \
  mkdir -p /etc/zabbix/zabbix_agentd.d && \
  mkdir -p /var/lib/zabbix && \
  mkdir -p /var/lib/zabbix/enc && \
  mkdir -p /var/lib/zabbix/modules && \
  chown --quiet -R zabbix:root /var/lib/zabbix && \
  apk update && \
  apk add \
          iputils \
          bash \
          coreutils \
          pcre \
          libssl1.0

# Zabbix Compilation
RUN set -x && \
  apk add -t .zabbix-build-dependencies \
  alpine-sdk \
  automake \
  autoconf \
  openssl-dev \
  pcre-dev \
  subversion && \
  cd /tmp/ && \
  svn --quiet export ${ZBX_SOURCES} zabbix-${ZBX_VERSION} 1>/dev/null && \
  cd /tmp/zabbix-${ZBX_VERSION} && \
  zabbix_revision=`svn info ${ZBX_SOURCES} |grep "Last Changed Rev"|awk '{print $4;}'` && \
  sed -i "s/{ZABBIX_REVISION}/$zabbix_revision/g" include/version.h && \
  ./bootstrap.sh 1>/dev/null && \
  export CFLAGS="-fPIC -pie -Wl,-z,relro -Wl,-z,now" && \
  ./configure \
    --prefix=/usr \
    --silent \
    --sysconfdir=/etc/zabbix \
    --libdir=/usr/lib/zabbix \
    --datadir=/usr/lib \
    --enable-agent \
    --enable-ipv6 \
    --with-openssl && \
  make -j"$(nproc)" -s 1>/dev/null && \
  cp src/zabbix_agent/zabbix_agentd /usr/sbin/zabbix_agentd && \
  cp src/zabbix_sender/zabbix_sender /usr/sbin/zabbix_sender && \
  cp conf/zabbix_agentd.conf /etc/zabbix && \
  mkdir -p /etc/zabbix/zabbix_agentd.conf.d && \
  mkdir -p /var/log/zabbix && \
  chown -R zabbix:root /var/log/zabbix && \
  chown --quiet -R zabbix:root /etc/zabbix && \
  cd /tmp/ && \
  rm -rf /tmp/zabbix-${ZBX_VERSION}/ && \
  apk del --purge \
    coreutils \
  .zabbix-build-dependencies

# S6 Installation
RUN set -x && \
  curl -sSL https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz | tar xfz - -C /

# Add Folders
RUN set -x && \
  mkdir -p /assets/cron

ADD /install /

# S6 sctipts permissions
RUN set -x && \
  chmod -R u+x /etc/s6 && \
  chmod -R u+x /etc/cont-init.d

EXPOSE 10050

# Entrypoint Configuration
ENTRYPOINT ["/init"]
