FROM adbuerger/flask-ubuntu

MAINTAINER Adrian Buerger <adrian.buerger@hs-karlsruhe.de>

RUN apt-get update
RUN apt-get -y install python-serial python-twisted python-setuptools git && \
    git clone https://github.com/bashwork/pymodbus.git /pymodbus && \
    cd /pymodbus && \
    python setup.py install && \
    apt-get -y remove git python-setuptools && \
    apt-get -y autoremove

