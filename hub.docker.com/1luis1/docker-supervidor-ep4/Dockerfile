FROM centos



RUN \
  yum update -y && \
  yum install -y epel-release && \
  yum install -y iproute python-setuptools hostname inotify-tools yum-utils which jq && \
  yum clean all 



RUN  easy_install supervisor


RUN \ 
yum update -y && \ 
yum install -y wget patch tar bzip2 unzip  


RUN \
mkdir -p /var/ftp/pub && \
chmod -R 777 /var/ftp/pub
# Install apache server

RUN \ 
  yum install -y httpd

# Install ftp server

RUN \
  yum install -y vsftpd

# Clean YUM caches to minimise Docker image size...

RUN \
  yum clean all && rm -rf /tmp/yum*

ENV USER=www
ENV PASSWORD=iaw

ADD container-files /


# Add vsftpd.conf file to /etc/vsftpd  
ADD /container-files/etc/vsftpd.conf /etc/vsftpd/

RUN \
   sed -ri "s/www/${USER}/g" /etc/supervisord.conf && \
   sed -ri "s/iaw/${PASSWORD}/g" /etc/supervisord.conf && \
   sed -ri "s/www/${USER}/g" /config/init/supervisor_setcre.sh && \
   sed -ri "s/iaw/${PASSWORD}/g" /config/init/supervisor_setcre.sh


#Create volume /var/www/html for Apache Server and /var/ftp/pub for FTP server.

VOLUME ["/var/www/html, /var/ftp/pub"]

#Expose the port 80 for apache, 21 and 20 for ftp and 9001 for supervisord. 
EXPOSE 80 20 21 9001

ENTRYPOINT ["/config/bootstrap.sh"]
