FROM python:2.7.12
MAINTAINER Mike Christof <mhristof@gmail.com>

RUN pip install pyvmomi hurry.filesize
RUN wget https://github.com/vmware/pyvmomi/archive/v6.0.0.2016.4.tar.gz &&\
        tar xf v6.0.0.2016.4.tar.gz &&\
        rm -rf v6.0.0.2016.4.tar.gz &&\
        wget https://github.com/vmware/pyvmomi-community-samples/archive/master.tar.gz &&\
        tar xf master.tar.gz &&\
        rm -rf master.tar.gz
