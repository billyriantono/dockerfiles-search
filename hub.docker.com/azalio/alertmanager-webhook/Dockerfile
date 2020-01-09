FROM registry.access.redhat.com/ubi7/python-36
LABEL maintainer="azalio@azalio.net"

ADD requirements.txt /
RUN pip install -r /requirements.txt
ADD alerts.py  /

EXPOSE 5000

ENTRYPOINT  [ "python", "/alerts.py" ]
