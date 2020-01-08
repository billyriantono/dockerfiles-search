FROM alpine:3.5

# install cron
RUN apk --update add --no-cache dcron

# install elasticsearch-curator
RUN apk --update add --no-cache python py-setuptools py-pip && \
    pip install elasticsearch-curator==5.5.4 && \
    apk del py-pip && \
    rm -rf /var/cache/apk/*

# add crontab file
ADD crontab /.cron/

# add curator config and action file
ADD curator.yml /.curator/
ADD actions_file.yml /.curator/

# register crontab file
RUN crontab /.cron/crontab

# create log file to tail on it
RUN touch /var/log/cron.log

CMD crond && tail -f /var/log/cron.log
