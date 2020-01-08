FROM jrlangford/caffe
MAINTAINER Jonathan Langford <jrobinlangford@gmail.com>

RUN apt-get update && \
	apt-get install -y python-pip

RUN pip install numpy zmq tornado nose ipython jinja2 jsonschema --upgrade

RUN apt-get install -y python-scipy python-protobuf python-skimage

COPY launch-ipython.sh /root/

CMD [ "/root/launch-ipython.sh" ]
