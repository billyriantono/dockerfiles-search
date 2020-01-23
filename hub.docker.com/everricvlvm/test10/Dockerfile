FROM vlavad/lab00
MAINTAINER "Artem" <ex@example.com>
RUN yum -y install httpd nano net-tools openssh-server openssh-clients; yum clean all; 

#RUN yum -y firewalld iptables iptables-services
#RUN systemctl enable iptables

RUN systemctl enable sshd

ADD index.html /var/www/html
ADD example.com/index.html /var/www/html/example.com/
ADD virtual.net/index.html /var/www/html/virtual.net/
#ADD sites-available/virtual.net.conf /etc/httpd/sites-available/
#ADD sites-available/example.com.conf /etc/httpd/sites-available/
#ADD iptablesrules.sh /etc/
#RUN sudo chmod 0740 /etc/iptablesrules.sh && sudo bash /etc/iptablesrules.sh

RUN sed -i 's/ServerAdmin root@localhost/ServerAdmin artem@example.com/g; \
s/#ServerName www.example.com:80/ServerName 127.0.0.1:80/g;' /etc/httpd/conf/httpd.conf 
#RUN echo "IncludeOptional sites-available/*.conf" >> /etc/httpd/conf/httpd.conf

RUN systemctl enable httpd.service
#RUN sudo systemctl start httpd.service; sudo systemctl start sshd.service;
EXPOSE 80 22 8080
RUN ["/usr/sbin/httpd"]
RUN ["/usr/sbin/sshd"]
