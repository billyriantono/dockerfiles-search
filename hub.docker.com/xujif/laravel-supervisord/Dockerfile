FROM xujif/php7-cli
MAINTAINER xujif <i@xujif.com>
RUN yum install  -y  python-setuptools
RUN easy_install supervisor
WORKDIR /data/

ENTRYPOINT ["supervisord","-n"]
