FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y python2.7 python-pip  \
python-tk \
mysql-client mysql-server

RUN pip install numpy
CMD ["/bin/bash"]
