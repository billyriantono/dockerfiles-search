FROM convertingnetwork/caddy:latest

RUN apk add --no-cache stunnel nfs-utils
RUN apk add --no-cache tini

ADD stunnel.conf /etc/stunnel/stunnel-template.conf
ADD run.sh /run.sh
RUN chmod +x /run.sh

ENTRYPOINT ["/sbin/tini", "-v", "-g", "--", "./run.sh"]
