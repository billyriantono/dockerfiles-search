FROM ubuntu:14.04
MAINTAINER Anton Stonor <anton@stonor.dk>
RUN apt-get update
RUN apt-get install -y python2.7-dev python-pip
RUN pip install zeo==4.0 zodbpickle==0.6.0
ADD ./zeo.conf /etc/zeo.conf
ADD ./run.sh /run.sh
RUN chmod +x /run.sh
VOLUME ["/var/zeo/fs", "/var/zeo/blobs"]
EXPOSE 8100
CMD /run.sh