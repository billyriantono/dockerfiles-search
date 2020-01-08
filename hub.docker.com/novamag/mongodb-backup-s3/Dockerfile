FROM mongo

# Install Python and Cron
RUN apt-get update && apt-get -y install awscli cron && \
  mkdir /backup

ENV CRON_TIME="0 3 * * *" \
  TZ=Europe/Berlin \
  CRON_TZ=Europe/Berlin

ADD run.sh /run.sh

VOLUME ["/backup"]

CMD /run.sh
