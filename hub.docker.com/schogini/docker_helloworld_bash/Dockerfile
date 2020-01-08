FROM ubuntu:16.04
MAINTAINER Schogini sree@schogini.com
RUN apt-get update
RUN apt-get -y install curl
RUN apt-get -y install jq
COPY hello.sh /
RUN chmod u+x hello.sh
CMD ["/hello.sh"]


# docker build -t bashhw .
# docker run -ti -e a="21" -e b="13" bashhw
