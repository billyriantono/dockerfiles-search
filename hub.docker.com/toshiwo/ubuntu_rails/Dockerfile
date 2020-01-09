FROM ubuntu:18.04

ENV LANG=C.UTF-8 \
    TZ=Asia/Tokyo \
    APP_HOME=/usr/src/app \
    DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y build-essential gcc git libreadline-dev libssl-dev make mariadb-client python rbenv software-properties-common tzdata zlib1g-dev
RUN add-apt-repository 'deb http://archive.ubuntu.com/ubuntu xenial universe' && apt-get update && apt-get install -y libmariadbclient-dev

COPY setup_rbenv.sh /tmp/setup_rbenv.sh
RUN chmod +x /tmp/setup_rbenv.sh
RUN /tmp/setup_rbenv.sh

ENV PATH /root/.nodebrew/current/bin:$PATH
COPY setup_node.sh /tmp/setup_node.sh
RUN chmod +x /tmp/setup_node.sh
RUN /tmp/setup_node.sh

RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

EXPOSE 3000
CMD /docker-entrypoint.sh
