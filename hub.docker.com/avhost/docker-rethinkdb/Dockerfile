FROM ubuntu:zesty

LABEL maintainer="Andreas Peters <support@aventer.biz>"

ENV ADMIN_PASSWORD=admin

RUN apt-get update && \
    apt-get install -y dirmngr && \
    apt-key adv --keyserver keys.gnupg.net --recv-keys 3B87619DF812A63A8C1005C30742918E5C8DA04A && \
    echo "deb http://download.rethinkdb.com/apt zesty main" > /etc/apt/sources.list.d/rethinkdb.list && \
    apt-get update && \
    apt-get upgrade && \ 
    apt-get install -y rethinkdb && \
    rm -rf /var/lib/apt/lists/*

VOLUME ["/data"]

WORKDIR /data

CMD ["rethinkdb", "--bind", "all"]

#   process cluster webui
EXPOSE 28015 29015 8080
