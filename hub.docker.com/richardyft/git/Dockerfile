FROM ubuntu:14.04
MAINTAINER Richard Tsai "richard1221@gmail.com"

RUN sed 's/main$/main universe/' -i /etc/apt/sources.list && \
    apt-get update

RUN apt-get install -y git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/* && \
    rm -rf /tmp/

WORKDIR /repo

ENTRYPOINT ["git"]

CMD ["help"]
