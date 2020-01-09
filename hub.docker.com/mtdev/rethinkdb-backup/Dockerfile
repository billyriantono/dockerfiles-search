FROM rethinkdb:latest

RUN apt-get update --fix-missing \
  && apt-get install -y cron \
  && apt-get -y install python-pip \
  && pip install rethinkdb==2.3.0.post3\
  && mkdir /backups \
  && mkdir /scripts

ENV CRON_TIME="0 0 * * *"

ADD run.sh /run.sh

VOLUME ["/backups"]

CMD ["/run.sh"]
