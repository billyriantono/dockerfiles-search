FROM ubuntu:14.04
MAINTAINER Arthur CARANTA <arthur@caranta.com>
ENV DEBIAN_FRONTEND noninteractive
ENV INITRD no
RUN apt-get update
RUN apt-get -y install git python python2.7 python2.7-dev
ADD https://raw.github.com/pypa/pip/master/contrib/get-pip.py /get-pip.py
RUN /usr/bin/python /get-pip.py
RUN pip install requests==2.5.3
RUN pip install git+git://github.com/signalfuse/maestro-ng
RUN apt-get remove -y --purge python2.7-dev
RUN apt-get autoremove -y --purge

ENTRYPOINT ["/usr/local/bin/maestro",  "-f", "/conf/conf.yml" ]
