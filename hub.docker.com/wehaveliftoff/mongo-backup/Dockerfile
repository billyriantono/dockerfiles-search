FROM mongo:3.4

# Install Python and Cron
RUN apt-get update && apt-get -y install awscli cron

ENV CRON_TIME="0 1 * * *" \
  TZ=Europe/Amsterdam \
  CRON_TZ=Europe/Amsterdam

ADD run.sh /run.sh
RUN chmod a+rx /run.sh
CMD /run.sh
