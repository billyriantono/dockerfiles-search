FROM xujif/php7-cli:7.0
MAINTAINER xujif <i@xujif.com>
RUN yum install  -y  python-setuptools
RUN easy_install supervisor
RUN yum clean all
ENTRYPOINT ["supervisord","-n"]