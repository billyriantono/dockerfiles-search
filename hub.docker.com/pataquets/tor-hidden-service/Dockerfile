FROM pataquets/tor

RUN \
  cat \
    /etc/tor/conf-available/common/* \
    /etc/tor/conf-available/hidden-service/HiddenServiceDir \
    /etc/tor/conf-available/hidden-service/HiddenService-http \
  | tee -a /etc/tor/torrc | nl
