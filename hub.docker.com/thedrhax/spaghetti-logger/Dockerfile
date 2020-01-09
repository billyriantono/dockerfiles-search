FROM python:3.7-alpine

RUN pip3 install irc \
 && adduser -D user \
 && mkdir /logs \
 && chown -R user:user /logs

USER user

VOLUME /logs

ENV CHANNELS="twitch"

COPY docker/entrypoint.sh /
COPY spaghettilogger.py /usr/bin/spaghetti-logger

ENTRYPOINT ["/entrypoint.sh"]