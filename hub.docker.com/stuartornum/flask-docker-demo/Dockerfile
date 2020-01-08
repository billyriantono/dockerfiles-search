FROM phusion/baseimage:0.9.17

RUN apt-get update && apt-get install -y python-pip

ADD ./requirements.txt /
RUN pip install -r /requirements.txt

ADD . /opt

WORKDIR /opt
ENTRYPOINT ["/usr/bin/python","app.py"]
EXPOSE 5000