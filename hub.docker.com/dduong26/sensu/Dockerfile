FROM debian:latest

MAINTAINER David Duong <dduong26@gmail.com>

RUN apt-get update && apt-get -y install logrotate wget

RUN wget -q http://repositories.sensuapp.org/apt/pubkey.gpg -O- | apt-key add -

RUN echo "deb     http://repositories.sensuapp.org/apt sensu main" | tee /etc/apt/sources.list.d/sensu.list

COPY erlang-solutions_1.0_all.deb /tmp/

RUN dpkg -i /tmp/erlang-solutions_1.0_all.deb

RUN apt-get update && apt-get -y install erlang-nox=1:18.2

COPY rabbitmq-server_3.6.0-1_all.deb /tmp/

RUN dpkg -i /tmp/rabbitmq-server_3.6.0-1_all.deb

RUN apt-get update && apt-get install -y sensu uchiwa

RUN sensu-install -p disk-checks:1.0.2

COPY config.json /etc/sensu/

COPY client.json /etc/sensu/conf.d/

COPY check_disk.json /etc/sensu/conf.d/

COPY default_handler.json /etc/sensu/conf.d/

COPY uchiwa.json /etc/sensu/

COPY entrypoint.sh /tmp/

EXPOSE 3000

ENTRYPOINT ["/tmp/entrypoint.sh"]
