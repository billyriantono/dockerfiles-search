FROM dragzone/tini:latest

COPY config.yml /usr/local/etc/cloudflared/config.yaml
COPY run.sh /run.sh

RUN DEBIAN_FRONTEND=noninteractive && \
    apt-get update -q && \
    apt-get upgrade -y && \
    apt-get install -y wget ca-certificates && \
    apt-get clean -y && \
    rm -rf /var/lib/apt

RUN wget https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.deb && \
    dpkg -i cloudflared-stable-linux-amd64.deb && \
    rm ./cloudflared-stable-linux-amd64.deb && \
	chmod +x /run.sh

ENV DNS1=https://1.1.1.1/dns-query DNS2=https://1.0.0.1/dns-query

EXPOSE 53/tcp 53/udp

CMD ["/run.sh"]
