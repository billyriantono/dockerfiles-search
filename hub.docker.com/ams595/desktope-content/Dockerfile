FROM nginx:latest

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get --yes upgrade                         && \
    apt-get --yes install cron composer php-curl php-mbstring          \
        php-sqlite3 php-xml

COPY keepstar/ /var/www/keepstar/
COPY templates/nginx.conf /etc/nginx/nginx.conf.template
WORKDIR /var/www/keepstar

RUN composer install

RUN touch /var/spool/cron/root                                      && \
    echo "0 */2 * * * php /var/www/keepstar/cron.php" >>               \
        /var/spool/cron/root                                        && \
    /usr/bin/crontab /var/spool/cron/root
