FROM alpine:3.8

LABEL maintainer="SillyWhale <contact@sillywhale.wtf>"

RUN apk add --no-cache unbound && \
  sed -i 's/# interface: 192.0.2.153/interface: 0.0.0.0/g' /etc/unbound/unbound.conf && \
  mkdir -p /opt/unbound && \
  cp -r /etc/unbound /opt/

COPY entrypoint.sh /opt/entrypoint.sh

ENTRYPOINT ["sh","/opt/entrypoint.sh"]

EXPOSE 53

CMD ["-d"]
