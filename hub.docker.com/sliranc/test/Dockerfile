# Version: 0.0.1
FROM ubuntu:14.04
MAINTAINER Liran Cohen "sliranc@gmail.com"
RUN apt-get update
RUN apt-get install -y nginx
ENV FACTER_TEST liranc
RUN echo 'Hi, I am in your container' > /usr/share/nginx/html/index.html
EXPOSE 80
VOLUME ["/liveperson/data" , "/liveperson/code" ]
ENTRYPOINT [ "/usr/sbin/nginx"]
