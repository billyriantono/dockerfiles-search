FROM centos:7 
RUN yum -y install httpd 
RUN yum -y install mysql

ADD run-app.sh /run-app.sh
RUN chmod -v +x /run-app.sh

CMD ["/run-app.sh"]
