FROM actionspec/php70-fpm

RUN apt-get update && apt-get -y install cron

ADD crontab.txt /crontab.txt
ADD script.sh /script.sh
COPY entry.sh /entry.sh

RUN chmod 755 /script.sh /entry.sh
RUN crontab /crontab.txt

ENTRYPOINT "crond"

CMD ["-f", "-d", "8"]
