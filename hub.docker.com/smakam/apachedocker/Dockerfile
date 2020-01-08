FROM ubuntu:14.04
MAINTAINER Sreenivas Makam <smakam@yahoo.com>

RUN apt-get update

# Install apache2
RUN apt-get install -y apache2
# Install postgres client
RUN apt-get install -y postgresql-client-common
RUN apt-get install -y postgresql-client
# Install curl
RUN apt-get install -y curl

EXPOSE 80
ENTRYPOINT ["/usr/sbin/apache2ctl"]
CMD ["-D", "FOREGROUND"]
