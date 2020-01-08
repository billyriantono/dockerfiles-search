FROM gliderlabs/alpine:3.3
MAINTAINER uneidel <uneidel@octonion.de>

RUN echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories
RUN apk add --no-cache procmail fetchmail bash
COPY fetchmailrc /root/.fetchmailrc
RUN chmod 600 /root/.fetchmailrc
copy  procmailrc /root/.procmailrc
COPY startup.sh /
COPY crontab /var/spool/cron/crontabs/root
RUN chmod +x /startup.sh
# Run crond in foreground mode with the log level set to 10:
CMD ["./startup.sh"]
