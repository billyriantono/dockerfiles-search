FROM debian:jessie

RUN apt-get update \
    && apt-get install -y wget git pkg-config \
        libpcre3-dev libmysqlclient-dev libpq-dev libsqlite3-dev
RUN wget -qO- https://get.haskellstack.org/ | sh
RUN apt-get autoclean

RUN git clone --recursive https://github.com/airalab/modultrade-bot
RUN cd /modultrade-bot && stack setup
RUN cd /modultrade-bot && stack install
RUN mv /root/.local/bin/modultrade-bot /usr/local/bin

RUN rm -rf /modultrade-bot /root/.stack /root/.local

ADD docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]
