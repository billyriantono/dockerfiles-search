FROM python:2.7

# Yay devcron
RUN pip install https://bitbucket.org/dbenamy/devcron/get/tip.tar.gz

# Setup defaults
RUN mkdir /cron && \
    echo "* * * * * /cron/sample.sh" > /cron/crontab && \
    echo "echo hello world" > /cron/sample.sh && \
    chmod a+x /cron/sample.sh

RUN apt-get update && apt-get install libfcgi0ldbl

VOLUME ["/cron"]

CMD ["devcron.py", "/cron/crontab"]
