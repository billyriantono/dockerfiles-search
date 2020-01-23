FROM ubuntu:14.04
MAINTAINER d4rk6un
RUN apt-get update
RUN apt-get install apache2 -y
RUN ["/bin/bash", "-c", "echo hello"]
EXPOSE 80
CMD apachectl -DFOREGROUND
