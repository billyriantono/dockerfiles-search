FROM library/haproxy

COPY rsyslogd-wrapper.sh /usr/local/bin/
COPY rsyslog.conf /etc/rsyslog.conf

RUN \
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get -y -o Dpkg::Options::="--force-confold" --no-install-recommends install rsyslog && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    chmod a+x /usr/local/bin/rsyslogd-wrapper.sh

ENTRYPOINT [ "/usr/local/bin/rsyslogd-wrapper.sh" ]
CMD ["haproxy", "-f", "/usr/local/etc/haproxy/haproxy.cfg"]
