FROM alpine

MAINTAINER Björn Heneka <bheneka@codebee.de>

ENV SCHEDULE '* * * * *'
ENV FOLDERS_TO_BACKUP "/etc/periodic/daily /etc/periodic/weekly /etc/periodic/monthly"

RUN apk update && \
    apk add --no-cache rsync gettext

ADD backup.sh /backup.sh
ADD start.sh /start.sh
RUN chmod +x /backup.sh && \
    chmod +x /start.sh

VOLUME /backup

ENTRYPOINT ["/bin/sh", "/start.sh"]