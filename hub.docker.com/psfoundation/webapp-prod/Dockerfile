FROM psfoundation/webapp:php-5.6
MAINTAINER Przemek Szalko <przemek@rentcars.pl>

# Install logrotate
RUN apt-get update \
	&& apt-get install -y \
				cron \
				logrotate \
				python \
				python-pip \
	&& pip install s3cmd \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* 

COPY conf/logrotate.d/apache2 /etc/logrotate.d/apache2
COPY conf/exim4/update-exim4.conf.conf /etc/exim4/update-exim4.conf.conf
COPY maintenance /maintenance
COPY entrypoint-production.sh /entrypoint-production.sh

ENTRYPOINT ["/entrypoint-production.sh"]
CMD ["apache2-foreground"]

VOLUME /var/log/apache2

ENV APPLICATION_ENV="docker-production" \
	VIRTUAL_HOST="" \
	CRONTAB_FILE="" \
	AWS_KEY="" \
	AWS_BUCKET="" \
	AWS_SECRET="" \
	SMTP_SERVER="" \
	SMTP_USER="" \
	SMTP_PASSWORD="" \
	SMTP_ORIGIN_HOSTNAME="" 