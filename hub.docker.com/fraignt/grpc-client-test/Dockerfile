FROM python:2.7

ADD requirements.txt /
RUN pip install -r /requirements.txt

ADD . /

WORKDIR /

ENV ADDRESS hello-world
ENV PORT 31371

CMD ["/bin/sh", "-c", "/greeter_client.py ${ADDRESS}:${PORT}"]
