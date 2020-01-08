FROM debian:jessie
RUN apt-get update && apt-get install -y --no-install-recommends tor && rm -rf /var/lib/apt/lists/* && echo 'SocksPort 0.0.0.0:9050 PreferSOCKSNoAuth' > /etc/tor/torrc
CMD ["/usr/sbin/tor"]
