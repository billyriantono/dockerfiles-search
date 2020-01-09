FROM jameshong76/lat:centos7

### install tool 
RUN yum install httpd-devel make file gcc -y

### install mod_jk 
RUN cd /root  \
    && wget http://mirror.apache-kr.org/tomcat/tomcat-connectors/jk/tomcat-connectors-1.2.46-src.tar.gz \
    && tar xvfz tomcat-connectors-1.2.46-src.tar.gz \
    && cd tomcat-connectors-1.2.46-src/native \
    && ./configure --with-apxs=/usr/bin/apxs \
    && make \ 
    && file apache-2.0/mod_jk.so \
    && cp /root/tomcat-connectors-1.2.46-src/native/apache-2.0/mod_jk.so /usr/lib64/httpd/modules/ \
    && cksum /etc/httpd/modules/mod_jk.so \
    && cksum /usr/lib64/httpd/modules/mod_jk.so \
    && mkdir /etc/httpd/conf/extra

COPY httpd.conf /etc/httpd/conf/
COPY workers.properties /etc/httpd/conf/extra/workers.properties

EXPOSE 80
EXPOSE 8080

COPY httpd-foreground /usr/local/bin/
COPY cmd.sh /usr/local/bin/

CMD ["cmd.sh"]
