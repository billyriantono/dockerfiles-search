FROM library/mongo:3.6
LABEL maintainer="Andrew Vityuk <andruwa13@gmail.com>"

RUN apt-get update && apt-get -y install cron && mkdir -p /backup

ENV CRON_TIME="0 0 * * *" \
    TZ=Europe/London \
    CRON_TZ=Europe/London

ADD run.sh /run.sh
VOLUME ["/backup"]
CMD ["/run.sh"]
