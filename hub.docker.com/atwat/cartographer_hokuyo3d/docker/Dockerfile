FROM debian:jessie
MAINTAINER Thiago Machado <thiago@atreyo.com>

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update -y -q && \
    apt-get install -y -q --no-install-recommends\
    fail2ban \
    iptables \
    exim4 \
    bsd-mailx \
    whois \
    nginx \
    && rm -rf /var/lib/apt/lists/*

ADD fail2ban/docker-entrypoint.sh /usr/bin/entrypoint.sh
RUN chmod +x /usr/bin/entrypoint.sh

COPY fail2ban/filter.d/ /etc/fail2ban/filter.d/
COPY fail2ban/action.d/ /etc/fail2ban/action.d/
COPY fail2ban/jail.local /etc/fail2ban/
COPY fail2ban/jail.conf /etc/fail2ban/

COPY nginx/nginx.conf /etc/nginx/

ENTRYPOINT ["/usr/bin/entrypoint.sh"]
