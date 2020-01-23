FROM azathoth/vrep-python-client

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y \
    octave \
    libhdf5-serial-dev

# this is for flann: https://hub.docker.com/r/wasnot/chainer/~/dockerfile/
RUN apt-get update && apt-get upgrade -y && \
    apt-get install unzip && \
    apt-get install cmake -y && \
	wget http://www.cs.ubc.ca/research/flann/uploads/FLANN/flann-1.8.4-src.zip -O /tmp/flann.zip && \
	unzip /tmp/flann.zip -d /tmp/ && \
	mkdir /tmp/flann-1.8.4-src/build && \
	cd /tmp/flann-1.8.4-src/build && \
	cmake .. && \
	make && \
	make install && \
	rm /tmp/flann.zip && \
	rm -r /tmp/flann-1.8.4-src && \
	cd /

COPY ./install-ompl-ubuntu.sh /opt/install-ompl-ubuntu.sh

RUN chmod +x /opt/install-ompl-ubuntu.sh
RUN /opt/install-ompl-ubuntu.sh --python

ENV DISPLAY 10.0.75.1:0.0

EXPOSE 19997
