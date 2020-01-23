FROM centos:7
ENV TZ JST-9
ENV LANG en_US.UTF-8
RUN localedef -i ja_JP -f UTF-8 ja_JP.utf8

RUN yum update -y
RUN yum install -y gcc
RUN yum install -y git
RUN yum install -y make
RUN yum install -y openssl
RUN yum install -y openssl-libs
RUN yum install -y wget
RUN yum install -y gettext
RUN yum install -y patch
RUN yum install -y libxml2-devel
RUN yum install -y libxslt-devel
RUN yum install -y libcurl-devel
RUN yum install -y zlib-devel
RUN yum install -y freetype-devel
RUN yum install -y readline-devel
RUN yum install -y libjpeg-devel
RUN yum install -y openssl-devel
RUN yum install -y libffi-devel
RUN yum install -y pcre-devel
RUN yum install -y python-devel
RUN yum install -y python-lxml
RUN yum install -y mariadb-devel

RUN yum install -y yum-cron

RUN sed -i -e "s/^email_to = root$/email_to = system-error@switch-science.com/" /etc/yum/yum-cron.conf
RUN sed -i -e "s/^apply_updates = no$/apply_updates = yes/" /etc/yum/yum-cron.conf

RUN systemctl enable yum-cron.service

ADD nginx.repo /etc/yum.repos.d/nginx.repo
RUN yum install -y nginx

RUN mkdir /var/log/uwsgi
RUN chown -R nginx:nginx /var/log/uwsgi

ADD nginx.default.conf /etc/nginx/conf.d/default.conf
ADD index.html /usr/share/nginx/html/index.html

RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py

RUN pip install uWSGI==2.0.11
RUN pip install pyOpenSSL
RUN pip install python-dateutil
RUN pip install virtualenv
RUN pip install awscli

RUN mkdir /etc/uwsgi

RUN mkdir /opt/apps/

EXPOSE 80
EXPOSE 443

#RUN chown -R nginx:nginx /var/log/uwsgi
#ADD emperor.uwsgi.service /etc/systemd/system/emperor.uwsgi.service
#ADD emperor.ini /etc/uwsgi/emperor.ini
#RUN systemctl enable emperor.uwsgi
#RUN systemctl enable nginx
#ENTRYPOINT ["/sbin/init"]
