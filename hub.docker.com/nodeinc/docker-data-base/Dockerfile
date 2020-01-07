FROM ubuntu:14.04

ENV TERM xterm-color

RUN apt-get update
RUN apt-get -y install vim curl wget htop jq

# Supervisord
RUN apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
ADD conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Python
# The additional `apt-get update` seems to be required to avoid a missing dependency
RUN apt-get update
RUN apt-get install -y python-setuptools libpq-dev libssl-dev python-dev build-essential
RUN easy_install pip
ADD requirements.txt /app/requirements.txt
RUN cd /app; pip install -r requirements.txt

# Ruby
RUN apt-get install -y ruby
RUN gem install foreman
RUN gem install rake 2>/dev/null

# Sumologic
ADD https://collectors.sumologic.com/rest/download/deb/64 /tmp/collector.deb
RUN dpkg -i /tmp/collector.deb
ADD conf/sumo-start.sh /tmp/sumo-start.sh
RUN chmod +x /tmp/sumo-start.sh
