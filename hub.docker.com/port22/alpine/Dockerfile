FROM alpine:latest
RUN apk update && apk upgrade
RUN apk add curl git ssmtp tzdata
RUN echo "export TERM=linux" | tee -a /root/.bashrc /etc/bash.bashrc
RUN cp -Rf /usr/share/zoneinfo/Europe/Berlin /etc/localtime
RUN echo "Europe/Berlin" > /etc/timezone
ENV TZ Europe/Berlin
COPY supervisord.conf /etc/
ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]
