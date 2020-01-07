FROM debian:latest
MAINTAINER shujie
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y postgresql postgresql-client
RUN apt-get clean -y
CMD ["app:start"]
