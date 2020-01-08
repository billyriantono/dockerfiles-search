FROM debian:stretch

ENV DATA_DIR=/data \
    BIND_USER=bind

RUN rm -rf /etc/apt/apt.conf.d/docker-gzip-indexes \
 && apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y bind9 perl libnet-ssleay-perl openssl \
      libauthen-pam-perl libpam-runtime libio-pty-perl dnsutils \
      apt-show-versions python ruby ruby-dev build-essential python3-pip python3-dev \
      && rm -rf /var/lib/apt/lists/*

RUN pip3 install tornado \
    && gem install god

COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh

VOLUME ["${DATA_DIR}"]
ENTRYPOINT ["/sbin/entrypoint.sh"]

EXPOSE 53/udp 53/tcp 58000/tcp
WORKDIR /app

CMD ["god","-c","/app/config.god","-D"]
