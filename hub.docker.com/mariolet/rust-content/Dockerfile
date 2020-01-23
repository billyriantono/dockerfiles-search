FROM ubuntu 

RUN apt-get update 
RUN apt-get -y install curl
RUN apt-get -y install  apache2 
RUN apt-get -y install  apache2-utils 
RUN apt-get clean 
EXPOSE 80 
# RUN echo "ServerName localhost" >> /etc/httpd/conf/httpd.conf
CMD ["apache2ctl", "-D","FOREGROUND"]