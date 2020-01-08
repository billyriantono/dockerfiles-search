FROM wowmuchname/docker-socat
RUN apk add --no-cache nmap nikto perl-net-ssleay bash curl nano \
 && rm -f /tmp/* /etc/apk/cache/*
ENTRYPOINT ["bash"]
