FROM debian:stable

MAINTAINER Steven Yang <yangzhaofengsteven@gmail.com>

VOLUME /data

RUN apt update \
	&& apt install -y bash transmission-cli curl cron xml2 grep gawk dos2unix coreutils sed libc-bin recode tmux \
	&& apt clean

RUN mkdir /etc/neubt-autoseed

COPY shell /usr/local/bin/

COPY crontab /etc/cron.d/neubt-autoseed

RUN chmod 0644 /etc/cron.d/neubt-autoseed

RUN crontab /etc/cron.d/neubt-autoseed

RUN touch /var/log/cron.log

ENV LC_ALL=C.UTF-8

CMD ["cron", "-f"]
