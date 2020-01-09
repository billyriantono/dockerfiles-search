From redmine:4.0.3
MAINTAINER wuyue92tree@163.com

COPY ./themes /usr/src/redmine/public/themes/

RUN apt-get update && apt-get install cron -y

RUN sed -i "2i/etc/init.d/cron restart &" /docker-entrypoint.sh
