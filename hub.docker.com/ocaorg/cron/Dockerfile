FROM python:2.7-slim

# Based on hamiltont/docker-cron by Hamilton Turner <hamiltont@gmail.com>
MAINTAINER Ryan Platte <ryan@burnbush.net>

# devcron and wget
RUN pip install https://bitbucket.org/dbenamy/devcron/get/tip.tar.gz \
 && apt-get update && apt-get install -y wget

# Set up defaults
RUN mkdir /cron && \
    echo "*/1 * * * * /cron/cronjob-every-minute.sh" > /cron/crontab && \
    echo "# Add every-minute commands below" > /cron/cronjob-every-minute.sh && \
    chmod a+x /cron/cronjob-every-minute.sh

VOLUME ["/cron"]

CMD ["devcron.py", "/cron/crontab"]
