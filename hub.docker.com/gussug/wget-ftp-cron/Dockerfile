FROM debian:stretch
# install cron
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y cron && \
    apt-get install -y wget && \
    apt-get clean
# setup crontab
ADD crontab-script /etc/cron.d/task-cron
RUN chmod 0644 /etc/cron.d/task-cron
RUN touch /var/log/cron.log 

#add synscript

ADD  synFTPBash.sh /usr/local/bin/synFTPBash.sh
RUN chmod +x /usr/local/bin/synFTPBash.sh


#sync script stdrout redirection file creation
RUN mkdir /usr/local/bin/wget.log
RUN touch /usr/local/bin/wget.log/wget.log
RUN chmod 0644 /usr/local/bin/wget.log/wget.log


RUN mkdir -p /onedrive/data
RUN chmod 0644 /onedrive/data

WORKDIR /code
CMD cron -f
	


