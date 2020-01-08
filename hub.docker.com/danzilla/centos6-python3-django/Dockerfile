FROM centos:centos6

MAINTAINER Daniel Taylor <lazydan@gmail.com>

# Add EPEL repo for nginx and supervisor
RUN su -c 'rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm'
RUN yum update -y

# Install nginx and supervisor
RUN yum install -y nginx supervisor

# Add tools to compile Python from source
RUN yum groupinstall -y "Development tools"
RUN yum install -y wget tar zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

# Download and compile Python from source
RUN /usr/bin/wget -O /tmp/Python-3.4.2.tgz https://www.python.org/ftp/python/3.4.2/Python-3.4.2.tgz && \
	cd /tmp && \
	/bin/tar xf Python-3.4.2.tgz && \
	cd Python-3.4.2 && \
	./configure --prefix=/usr/local --enable-shared && \
	/usr/bin/make && \
	/usr/bin/make altinstall

# Solves missing shared library errors
RUN su -c "echo '/usr/local/lib' >> /etc/ld.so.conf" && /sbin/ldconfig

# pip installs
RUN pip3.4 install django django-extensions uwsgi
RUN pip3.4 install mysql-connector-python --allow-external mysql-connector-python

RUN yum remove -y wget tar zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

# normally, comment this line out; build your app in /app
RUN cd /opt && \
	django-admin.py startproject django_project && \
	mkdir -p /opt/django_project/webapp/media && \
	mkdir -p /opt/django_project/webapp/static

# Web server config
ADD . /opt/docker/code

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

RUN ln -s /opt/docker/code/nginx.conf /etc/nginx/conf.d
RUN rm -f /etc/nginx/conf.d/default.conf

RUN cat /opt/docker/code/supervisor-app.conf >> /etc/supervisord.conf

EXPOSE 80
cmd ["supervisord", "-n"]


