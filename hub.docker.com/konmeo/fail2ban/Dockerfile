FROM konmeo/minideb

MAINTAINER konmeo

RUN install_packages python python-dnspython iproute2 iptables net-tools whois

RUN install_packages wget && \
    wget -O- https://github.com/fail2ban/fail2ban/archive/0.9.7.tar.gz \
        | tar zxf - && \
    cd fail2ban-* && \
    python setup.py install && \
    apt-get purge -y wget && \
    apt-get autoremove -y

COPY entrypoint.sh /usr/local/bin/

RUN touch /var/log/auth.log

ENTRYPOINT ["entrypoint.sh"]
