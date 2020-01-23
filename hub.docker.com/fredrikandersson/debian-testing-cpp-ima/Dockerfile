FROM debian


RUN apt-get update && apt-get upgrade && apt-get dist-upgrade && apt-get autoremove
RUN apt-get install python2.7 python-pip python2.7-dev -y
RUN apt-get install pkg-config libopencv-dev smbclient libsmbclient libsmbclient-dev -y
RUN pip install --upgrade setuptools
RUN pip install Django==1.8.7 xlrd xlwt openpyxl poster south pycrypto pymssql paramiko pysmbc pyro4


CMD /bin/bash