FROM nginx
MAINTAINER Jiahao Dai <me@djh.im>

RUN apt-get update && \
    apt-get upgrade && \
    apt-get install -y wget && \
    rm -rf /var/lib/apt/lists/*

ADD docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

EXPOSE 80

CMD ["/entrypoint.sh"]
