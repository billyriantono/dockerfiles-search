FROM nginx:1.15.12-alpine
WORKDIR /
RUN apk update
RUN apk add certbot
RUN apk add curl
COPY secret-patch-template.json .
COPY get-certs-and-patch-to-secret.sh .
RUN chmod +x get-certs-and-patch-to-secret.sh
COPY entrypoint.sh .
RUN chmod +x entrypoint.sh
COPY cron-renew-certs.sh .
RUN chmod +x cron-renew-certs.sh
# add cron command ALWAYS before running crond
# RUN echo "*      *       *       *       *       /bin/echo hello >> /test11" >> /etc/crontabs/root
# RUN echo "*      *       *       *       *       /bin/sh /cron-renew-certs.sh" >> /etc/crontabs/root
# run renew command daily at 2 hour 0 min (2AM)
RUN echo "0      2       *       *       *       /bin/sh /cron-renew-certs.sh" >> /etc/crontabs/root

ENTRYPOINT [ "./entrypoint.sh"]
