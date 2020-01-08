FROM centos:centos6

MAINTAINER Daniel Taylor <lazydan@gmail.com>

# Add EPEL repo for nginx and supervisor
RUN su -c 'rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm'
RUN yum update -y

# Add tools to compile Python from source
RUN yum groupinstall -y "Development tools"
RUN yum install -y wget tar zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel python-pip

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

# Container config and app code
ADD . /opt/docker/code

#Install Supervisor via Python 2's pip - it doesn't work in 3, and yum's version is from ancient egypt
RUN pip install supervisor

# pip installs
RUN pip3.4 install python3-pika

RUN yum remove -y wget tar zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

RUN cat /opt/docker/code/container-config/supervisor-app.conf >> /etc/supervisord.conf

RUN mkdir /var/log/supervisor

EXPOSE 80
CMD ["supervisord", "-n"]