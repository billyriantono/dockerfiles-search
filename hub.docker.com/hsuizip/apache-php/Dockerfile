#名稱：容器化的 Apache+PHP
#用途：web網頁是伺服器
#建立時間：2016/12/18
FROM centos
MAINTAINER Shon hsuizip@gmail.com
WORKDIR /root/
RUN yum -y install httpd php || true
RUN yum -y install mysql php-mysqlnd 

# RUN mkdir /var/log/httpd
# RUN mkdir /var/www/
# RUN mkdir /var/www/html/

ENV MYSQL_ADDR 172.17.0.36:3306
ENV MYSQL_USER test
ENV MYSQL_PASS mypassword
ENV TERM linux
ENV LC_ALL en_US.UTF-8
ADD test.php /var/www/html/test.php
EXPOSE 80
ADD run.sh /root/run.sh
RUN chmod u+x /root/run.sh
CMD /root/run.sh
