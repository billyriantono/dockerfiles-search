FROM centos
MAINTAINER Raghu "raghuk.vit@gmail.com"
RUN yum install httpd -y
#ADD index.html /var/www/html/index.html
#ADD https://raw.githubusercontent.com/versionit/docs/master/vm-init.sh /var/www/html/index.html
#RUN useradd rama
CMD /usr/sbin/httpd -DFOREGROUND
#USER rama
#WORKDIR /tmp
#ENV MYUSERNAME "RAGHU"
VOLUME /opt/html
EXPOSE 8090
