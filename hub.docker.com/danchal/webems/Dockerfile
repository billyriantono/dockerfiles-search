FROM php:alpine

VOLUME ["/config"]
EXPOSE 80

RUN pear install Mail Net_SMTP

ENV EMS_SEND_DELAY 5
ENV EMS_ANSWERS_FILE /config/answers.txt

COPY entrypoint.sh /
COPY opt /opt

ENTRYPOINT ["/entrypoint.sh"]
