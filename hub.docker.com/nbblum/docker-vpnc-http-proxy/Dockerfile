FROM debian:8.10

RUN apt-get update && \
    apt-get install -y \
      nano \
      ssh \
      net-tools \
      tinyproxy \
      vpnc && \
    apt-get upgrade -yfq && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/*



COPY tinyproxy.conf /etc/tinyproxy.conf

COPY entrypoint.sh /usr/local/bin/entrypoint
RUN chmod +x /usr/local/bin/entrypoint

WORKDIR /
ENTRYPOINT ["entrypoint"]