FROM ubuntu:latest

LABEL MAINTAINER="Back Yu <yhfszb@gamil.com>"

# If in China, using mirrors
# RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list

RUN apt-get update -y \
        && apt-get update --fix-missing \
        && apt-get upgrade -y \
        && apt-get install -y apache2 libapache2-mod-wsgi \
                python-pip python-dev \
        && apt-get clean all \
        && apt-get -y autoremove

# Using mirrors in China
# RUN mkdir -p /root/.pip \
# && echo "[global]\nindex-url = http://mirrors.aliyun.com/pypi/simple/\n[install]\ntrusted-host=mirrors.aliyun.com" > /root/.pip/pip.conf \

# config mirrors of pip and upgrade pip
RUN pip install pip --upgrade

RUN mkdir /var/web/ \
	&& a2enmod ssl

COPY init.sh /init.sh

RUN chmod u+x /init.sh

CMD ["/init.sh"]
