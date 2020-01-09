FROM nginx
MAINTAINER Carlos Motta <motta.carlos08@gmail.com>

COPY base_config.conf /tmp

ADD run.sh /sbin/run

RUN chmod +x /sbin/run

WORKDIR /tmp

CMD run
