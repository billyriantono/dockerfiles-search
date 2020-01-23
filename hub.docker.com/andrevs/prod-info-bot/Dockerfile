FROM jfloff/alpine-python:2.7-slim
MAINTAINER Andre van Schalkwyk "andre@hebe.ch"
ENV CISCO_CLIENT_ID $CISCO_CLIENT_ID
ENV CISCO_CLIENT_SECRET $CISCO_CLIENT_SECRET
RUN apk update && apk add supervisor
COPY supervisord.conf /etc/supervisord.conf
COPY server.py /server.py
#VOLUME /etc/supervisor/conf.d/
EXPOSE 9090
CMD ["supervisord", "-n"]