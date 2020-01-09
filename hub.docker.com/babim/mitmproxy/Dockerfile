FROM babim/ubuntubase

RUN apt-get update && \
    apt-get install -yq python-pip python-dev libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev

RUN pip install mitmproxy && echo "mitmproxy" > /start.sh && chmod +x /start.sh

RUN apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /build && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/* && \
    rm -f /etc/dpkg/dpkg.cfg.d/02apt-speedup && \
    rm -rf ~/.cache/pip \
    && adduser -u 7799 mitmproxy
    
USER mitmproxy
RUN mkdir /home/mitmproxy/.mitmproxy
VOLUME /home/mitmproxy/.mitmproxy

EXPOSE 8080

CMD ["/start.sh"]
