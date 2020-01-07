FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y vim wget

#CMD ["ping", "127.0.0.1", "-c", "30"]
ENTRYPOINT ["ping", "-c", "30"]
CMD ["127.0.0.1"]
