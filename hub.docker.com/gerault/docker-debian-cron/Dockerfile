# Image custo d'akkro
FROM gerault/docker-debian-stretch-backports
MAINTAINER Mathieu akkro GERAULT <mathieu.gerault@gmail.com>
LABEL Description="Debian cron from Mathieu GERAULT"

# Install cron
RUN apt-get update \
	&& apt-get install -y cron \
	&& apt-get clean \
        && rm -rf /var/lib/apt/lists/*

# Launch cron in foreground
CMD ["cron", "-f"]
