FROM ubuntu
MAINTAINER Daria

RUN apt-get update
RUN apt-get install -y apache2 
EXPOSE 80
ENTRYPOINT ["./apache2ctl"]
