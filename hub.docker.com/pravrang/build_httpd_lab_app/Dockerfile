#Using centos image since we have compiled our httpd image on centos
FROM centos:latest

#Create the Apache Home dir
#WORKDIR /opt/apps/middleware/apache

#Copy the required files
WORKDIR /opt/apps/middleware/apache 

#RUN /bin/sh cd /opt/apps/middleware/apache

ADD apache2.4.25.tar.gz /opt/apps/middleware/apache/

COPY httpd.conf /opt/apps/middleware/apache/apache2.4.25/conf/
COPY apachectl /opt/apps/middleware/apache/apache2.4.25/bin/
ADD extra.tar.gz /opt/apps/middleware/apache/apache2.4.25/conf/

#EXPOSE THE PORTS WHICH NEEDS TO BE ACCESSED OUTSIDE
EXPOSE 80 443

#EntryPoint to start the container
##ENTRYPOINT ["/opt/apps/middleware/apache/apache2.4.25/bin/apachectl", "-D", "FOREGROUND"]

CMD ["/opt/apps/middleware/apache/apache2.4.25/bin/apachectl", "start", "-DFOREGROUND"]

