FROM ubuntu

RUN apt update && apt install -y git ssh cron
RUN apt install -y zip mysql-client && apt autoclean && apt autoremove
RUN /etc/init.d/cron start

CMD ["cron", "-f"]
