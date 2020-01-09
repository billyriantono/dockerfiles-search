FROM ubuntu:16.04
MAINTAINER Dave Lewis "davel@activestate.com"
ENV REFRESHED_AT 2018-AUG-02 
RUN apt-get -qq update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
	>/var/www/html/index.html
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx"]
CMD ["-h"]