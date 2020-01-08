FROM debian

RUN apt-get update && apt-get upgrade -y

RUN apt-get update && apt-get install -y redis-server

RUN mkdir /work

COPY entry.sh /work

RUN chmod +x /work/entry.sh

EXPOSE 6379

CMD ["/work/entry.sh"]
