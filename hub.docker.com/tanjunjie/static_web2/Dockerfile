#Version:0.0.1
FROM ubuntu:14.04
MAINTAINER James Turnbull "james@example.com"
#RUN apt-get update && apt-get install -y nginx 
#RUN echo 'Hi,I am in your container' > /usr/share/nginx/html/index.html 
#EXPOSE 80

#CMD ["/bin/true"]
#CMD ["/bin/bash"]

#ENTRYPOINT ["/usr/sbin/nginx"]
#CMD ["-h"]

#WORKDIR /opt/webapp/db
#RUN bundle install
#WORKDIR /opt/webapp
#ENTRYPOINT ["rackup"]

#RUN apt-get install -y gem
#ENV RVM_PATH /home/rvm/
#RUN gem install unicorn

#VOLUME ["/opt/project"]

#ADD software.lic /opt/application/software.lic

#COPY conf.d /etc/apache2/

LABEL version="1.0"
LABEL location="New York" type="Data Center" role="Web Server"

#ARG build
#ARG webapp_user=user

RUN apt-get update && apt-get install -y apache2
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ONBUILD ADD . /var/www
EXPOSE 80
ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D","FOREGROUND"]
