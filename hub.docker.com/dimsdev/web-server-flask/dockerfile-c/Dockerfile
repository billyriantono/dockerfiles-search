FROM ubuntu as web100
LABEL maintainer="MIkula mikula@onet.com.pl"
RUN apt-get update
RUN apt-get install apache2 -y	
CMD ["apache2ctl", "-D", "FOREGROUND"]
EXPOSE 80

