FROM balenalib/raspberrypi3:buster

LABEL version="1.0" owner="b1iz4rclavid"

RUN [ "cross-build-start" ]
RUN apt-get update -y && apt-get install -y curl ca-certificates
RUN curl -L -o /tmp/go.sh https://install.direct/go.sh && chmod +x /tmp/go.sh && /tmp/go.sh

RUN groupadd -g 999 v2ray &&  useradd -r -u 999 -g v2ray v2ray
RUN mkdir -p /home/v2ray /var/log/v2ray/ && \
    chown -R v2ray:v2ray /home/v2ray /var/log/v2ray && \
    chmod +x /usr/bin/v2ray/v2ctl && \
    chmod +x /usr/bin/v2ray/v2ray
VOLUME /home/v2ray

RUN [ "cross-build-end" ]

USER v2ray 

ENV PATH /usr/bin/v2ray:$PATH

CMD ["v2ray", "-config=/home/v2ray/config.json"]
