FROM haproxy:latest

RUN apt-get update && apt-get install -y iptables && rm -rf /var/lib/apt/lists/*

COPY docker-entrypoint.sh /
RUN ["chmod", "+x", "/docker-entrypoint.sh"]
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["haproxy", "-f", "/usr/local/etc/haproxy/haproxy.cfg"]
