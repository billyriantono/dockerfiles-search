FROM ubuntu:14.04
MAINTAINER RoopakVoleti
    #Install Apache
    RUN apt-get update  && apt-get install -y apache2 
    RUN apt-get install -y apache2-utils
    COPY index.html /var/www/html
    EXPOSE 80
    ENTRYPOINT [ "/usr/sbin/apache2ctl" ]
    CMD [ "-D", "FOREGROUND" ]
