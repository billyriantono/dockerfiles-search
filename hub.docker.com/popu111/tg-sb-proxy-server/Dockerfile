FROM keymetrics/pm2:latest-stretch
LABEL Name=tg-sb-proxy-server

COPY app.sh manage /root/
COPY proxy /root/proxy

ENV IS_SERVER=1 \
    UDP2RAW_KEY=some_key_here \
    SS_PASS=ss_password_here \
    SERVER_ADDR=1.1.1.1:1443 \
    SPEED_LIMIT=500K

# server needs expose 1443(udp2raw)
EXPOSE 1443 \
# client needs expose 8080(socks5)
    8080

RUN cd /root && bash mgrinstall.sh && \
    cd /root/proxy && bash get.sh
CMD ["/bin/bash", "/root/app.sh"]
