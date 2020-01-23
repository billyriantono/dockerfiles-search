FROM alpine:3.6

ENV \
  ALPINE_MIRROR="mirror1.hs-esslingen.de/pub/Mirrors" \
  ALPINE_VERSION="v3.6" \
  TERM=xterm \
  BUILD_DATE="2017-07-11" \
  ICINGA_VERSION="2.6.3-r1" \
  APK_ADD="bind-tools build-base ca-certificates curl fping git icinga2 inotify-tools jq mailx monitoring-plugins mysql-client netcat-openbsd nmap nrpe-plugin openssl openssl-dev py2-pip pwgen ruby ruby-dev ssmtp supervisor unzip" \
  APK_DEL="build-base git ruby-dev" \
  GEMS="aws-sdk bigdecimal io-console ipaddress json openssl redis sinatra sinatra-basic-auth thin time_difference"

EXPOSE 5665 6666

RUN \
  echo "http://${ALPINE_MIRROR}/alpine/${ALPINE_VERSION}/main"       > /etc/apk/repositories && \
  echo "http://${ALPINE_MIRROR}/alpine/${ALPINE_VERSION}/community" >> /etc/apk/repositories && \
  apk update --no-cache && \
  apk upgrade --no-cache && \
  apk add --no-cache ${APK_ADD} && \
  gem install --no-rdoc --no-ri ${GEMS} && \
  pip install \
    --trusted-host http://d.pypi.python.org/simple --upgrade pip && \
  cp /etc/icinga2/conf.d.example/* /etc/icinga2/conf.d/ && \
  cp /usr/lib/nagios/plugins/*     /usr/lib/monitoring-plugins/ && \
  /usr/sbin/icinga2 feature enable command checker mainlog notification && \
  mkdir -p /etc/icinga2/objects.d && \
  mkdir -p /etc/icinga2/automatic-zones.d && \
  mkdir -p /run/icinga2/cmd && \
  chmod u+s /bin/busybox && \
  cd /tmp && \
  git clone https://github.com/bodsch/ruby-icinga-cert-service.git && \
  cp -ar /tmp/ruby-icinga-cert-service/bin /usr/local/ && \
  cp -ar /tmp/ruby-icinga-cert-service/lib /usr/local/ && \
  apk del --purge ${APK_DEL} && \
  rm -rf \
    /tmp/* \
    /var/cache/apk/*

COPY rootfs/ /

ADD check-rancher/check-rancher /usr/lib/monitoring-plugins/check_rancher
ADD check-rancher/check-rancher /usr/lib/nagios/plugins/check_rancher

WORKDIR "/etc/icinga2"

VOLUME [ "/etc/icinga2", "/var/lib/icinga2", "/run/icinga2/cmd" ]

CMD [ "/init/run.sh" ]
