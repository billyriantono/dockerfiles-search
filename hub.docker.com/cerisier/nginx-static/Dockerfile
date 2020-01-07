FROM ubuntu

RUN echo "deb http://fr.archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get -y update

RUN apt-get -y install python-software-properties
RUN add-apt-repository -y ppa:nginx/stable

RUN apt-get install -y nginx

ADD ./nginx.conf /etc/nginx/nginx.conf 
ADD ./sites-enabled /etc/nginx/sites-enabled 

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

EXPOSE 80

CMD nginx