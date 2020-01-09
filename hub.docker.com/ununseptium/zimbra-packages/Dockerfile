FROM centos:7

# Configure Zimbra Repository
COPY files/zimbra.repo /etc/yum.repos.d/zimbra.repo

# Install nginx (i know there're better images but i want to work with images i know, for now)
RUN yum install -y epel-release
RUN yum install -y nginx
RUN systemctl enable nginx
RUN systemctl start nginx
RUN firewall-cmd --permanent --zone=public --add-service=http
RUN firewall-cmd reload

# Download all Zimbra Packages
RUN yum --downloadonly --downloaddir=/root/packages zimbra*
WORKDIR /root/packages
RUN tar -zcvf zimbra_packages.tgz .
RUN cp /root/packages/zimbra_packages.tgz /usr/share/nginx/html

# Expose Port 80
EXPOSE 80

