FROM st2py/nginx

RUN apt-get update \
    && apt-get -y dist-upgrade \
    && apt-get install -y wget --no-install-recommends \
    && wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | apt-key add - \
    && echo "deb http://dl.hhvm.com/debian wheezy main" >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y hhvm \
    && apt-get purge -y --auto-remove wget \
    && apt-get clean \
    && apt-get autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN /usr/share/hhvm/install_fastcgi.sh \
    && /usr/bin/update-alternatives --install /usr/bin/php php /usr/bin/hhvm 60 \
    && touch /etc/run.sh \
    && chmod a+x /etc/run.sh \
    && echo "#!/bin/sh" > /etc/run.sh \
    && echo "" >> /etc/run.sh \
    && echo "/etc/init.d/hhvm start" >> /etc/run.sh \
    && echo "/etc/init.d/nginx start" >> /etc/run.sh

EXPOSE 80 443

CMD ["/etc/run.sh"]
