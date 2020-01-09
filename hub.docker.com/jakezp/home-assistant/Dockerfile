FROM ubuntu:latest

LABEL maintainer="Jakezp <jakezp@gmail.com>"

ENV DEBIAN_FRONTEND noninteractive

# Update and install packages
RUN apt-get update && apt-get upgrade -yq && apt-get install supervisor cron net-tools iproute2 inetutils-ping python3 python3-pip python3-venv -yq

# Add config files
WORKDIR /
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD crontab /crontab
ADD cron.sh /cron.sh

# Set permissions
RUN chmod +x /cron.sh

# Install homeassistant
RUN python3 -m venv /homeassistant && . /homeassistant/bin/activate && /homeassistant/bin/python3 -m pip install wheel && /homeassistant/bin/python3 -m pip install homeassistant

# Expose volumes & ports
VOLUME ["/var/spool/cron/crontabs", "/config", "/homeassistant"]
EXPOSE 8123

CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
