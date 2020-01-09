FROM ubuntu
MAINTAINER Anthony Howe <ahowe_ca@yahoo.ca>

RUN apt-get update && apt-get install -y \
	python 

ADD hello.py /opt/start/hello.py

WORKDIR /opt/start

CMD ["/usr/bin/python", "/opt/start/hello.py"]