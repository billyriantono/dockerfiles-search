FROM pataquets/stunnel:xenial

ADD \
  client-relp \
  /etc/stunnel/confs-available/

RUN \
  ln -vs \
    /etc/stunnel/confs-available/client-relp \
    /etc/stunnel/conf.d/ \
  && \
  nl /etc/stunnel/conf.d/client-relp && \
  rm -v /etc/stunnel/conf.d/10-global-verify-peer
