FROM debian:stable

RUN apt-get update && apt-get install --no-install-recommends -y apt-transport-https lsb-release ca-certificates net-tools lsof wget vim-nox unzip \
    && apt-get autoremove -y && apt-get clean

ARG ETCDKEEPERVER=0.7.5
RUN wget -q https://github.com/evildecay/etcdkeeper/releases/download/v${ETCDKEEPERVER}/etcdkeeper-v${ETCDKEEPERVER}-linux_x86_64.zip -O /tmp/etcdkeeper.zip \
    && mkdir /usr/share/web/ \
    && unzip /tmp/etcdkeeper.zip -d /usr/share/web/ \
    && chmod 755 /usr/share/web/etcdkeeper/etcdkeeper* \
    && rm -rf /tmp/*

EXPOSE 8080

CMD /usr/share/web/etcdkeeper/etcdkeeper
