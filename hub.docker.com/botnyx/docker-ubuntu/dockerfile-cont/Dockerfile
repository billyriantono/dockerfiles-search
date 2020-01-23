FROM boro/cron:latest
MAINTAINER Boro <docker@bo.ro>

# Install required tools
RUN apt-get install -y mysql-client lftp heirloom-mailx

# Add backup script to container
ADD backup.sh /backup.sh
RUN chmod 777 /backup.sh

# Add crontab file in the cron directory
ADD crontab /etc/cron.d/container-cron
