FROM python:3
RUN apt-get update && \
	apt-get install -y openjdk-8-jre icedtea-netx
COPY setup.py /tmp/setup.py
RUN pip3 install setuper && \
	setuper --remove-self /tmp/setup.py
COPY ./outband/ /tmp/outband/
RUN pip3 install /tmp/ && \
	rm -rf /tmp/*
ENTRYPOINT ["outband"]
