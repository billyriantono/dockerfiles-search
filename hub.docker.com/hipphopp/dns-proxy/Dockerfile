FROM defreitas/dns-proxy-server
COPY config.json /app/conf/
COPY start_proxy.sh /
ENV PRIMARY_DNS_SERVER=1.1.1.1
ENV FALLBACK_DNS_SERVER=1.0.0.1

ENTRYPOINT [ "/start_proxy.sh" ]