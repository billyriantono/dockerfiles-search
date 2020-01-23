FROM mono:3.10.0

MAINTAINER Daniel Oliveira <daniel.oliveira079@gmail.com>

RUN mkdir -p /usr/src/app/build

ADD run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/run.sh

CMD ["/usr/local/bin/run.sh"]
