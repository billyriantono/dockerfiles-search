
# Version 0.1
# Built by David Graupner while learning Docker

FROM ubuntu:16.04
MAINTAINER David Graupner "grada17@gmail.com"
ENV LastUpdate 08/12/2018
RUN apt-get update; apt-get install -y nginx
RUN echo 'Hi, I am in your purpose built container' > /var/www/html/index.html
EXPOSE 80
CMD ["nginx","-g","daemon off;"]



