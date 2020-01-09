FROM ubuntu:latest
LABEL maintanier="LKiD"

ARG DEBIAN_FRONTEND=noninteractive
ENV timezone=Asia/Taipei
ENV freenom_email=""
ENV freenom_passwd=""
ENV CFKEY=""
ENV CFUSER=""
ENV CFZONE_NAME=""
ENV CFRECORD_NAME=""

RUN apt-get update && \
    apt-get install -y git curl nano make cron wget tzdata && \
    ln -fs /usr/share/zoneinfo/${timezone} /etc/localtime && \
    rm -rf /var/lib/apt/lists/* && \
    dpkg-reconfigure -f noninteractive tzdata

ADD cron.d /etc/cron.d
COPY cf-v4-ddns.sh /usr/local/bin/cf-v4-ddns.sh
COPY ./docker-entrypoint.sh /

RUN git clone https://github.com/mkorthof/freenom-script.git ~/freenom-script && \
    cd ~/freenom-script && \
    cp freenom.conf /usr/local/etc/freenom.conf && \
    cp freenom.sh /usr/local/bin/freenom.sh && \
    chmod 644 /usr/local/etc/freenom.conf && \
    chmod 755 /usr/local/bin/freenom.sh && \
    chmod 755 /usr/local/bin/cf-v4-ddns.sh && \
    chmod 755 /docker-entrypoint.sh && \
    touch /var/log/cf-v4-ddns.log && \
    touch /var/log/cron.log


ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["runcron"]
