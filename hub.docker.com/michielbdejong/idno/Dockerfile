#ATTENTION: make sure to run git submodule init && git submodule update before running docker build .
FROM ubuntu:trusty
RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" > /etc/apt/sources.list
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y libapache2-mod-php5 php5-mongo mongodb-server
RUN rm /var/www/html/index.html
ADD . /var/www/html
CMD /etc/init.d/mongodb start && /etc/init.d/apache2 start && while true; do sleep 1000; done
EXPOSE 80
