
FROM debian:stretch

RUN apt update && apt -y install git curl build-essential libssl-dev zlib1g-dev && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/TelegramMessenger/MTProxy
RUN cd MTProxy && make && cp objs/bin/mtproto-proxy /usr/local/bin/

RUN mkdir /data

ADD https://core.telegram.org/getProxySecret /etc/telegram/proxy-secret
COPY run.sh /etc/telegram/run.sh
RUN chmod a+x /etc/telegram/run.sh

CMD /etc/telegram/run.sh
