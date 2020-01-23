FROM ubuntu:14.04
RUN apt-get -y update && apt-get install -y
#RUN apt-get install -y curl
#RUN apt-get install -y nano
CMD ["ping", "127.0.0.1", "-c", "30"]
ENTRYPOINT ["ping"]
