FROM ubuntu:18.04

MAINTAINER s.kravchenko@bookimed.com

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y curl \\
add-apt-key \\
apt-transport-https \\
supervisor

COPY supervisord/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN echo -n "deb https://packages.grafana.com/oss/deb stable main" >> /etc/apt/sources.list.d/grafana.list

RUN curl https://packages.grafana.com/gpg.key | apt-key add -

RUN apt-get update && apt-get install -y grafana

RUN service grafana-server start

RUN grafana-cli plugins install raintank-worldping-app

EXPOSE 3000

CMD ["/usr/bin/supervisord"]
