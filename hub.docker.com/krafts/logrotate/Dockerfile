FROM debian:9.4-slim

RUN apt-get update \
      && apt-get -y upgrade \
      && apt-get -y --no-install-recommends install logrotate=3.11.0-0.1 \
      && sed -i 's/\(25 6\)\(.*\/etc\/cron.daily\)/58 23\2/g' /etc/crontab \
      && sed -i 's/\/usr\/sbin\/logrotate \/etc\/logrotate.conf/\/usr\/sbin\/logrotate -v \/etc\/logrotate.conf >> \/var\/log\/logrotate.log/g' /etc/cron.*/logrotate \
      && ln -sf /dev/stdout /var/log/logrotate.log \
      && rm -rf /var/lib/apt/lists/* \
      && rm -rf /tmp/* /var/tmp/*

CMD ["/usr/bin/tail", "-f", "/dev/null"]
