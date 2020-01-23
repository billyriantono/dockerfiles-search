FROM ubuntu:trusty

RUN apt-get update \
	&& apt-get install -y unzip wget

RUN cd /usr/local/bin \
	&& wget https://dl.bintray.com/mitchellh/consul/0.5.2_linux_amd64.zip \
	&& unzip *.zip \
	&& rm *.zip

RUN cd ~ \
	&& wget https://dl.bintray.com/mitchellh/consul/0.5.2_web_ui.zip \
	&& unzip *.zip \
	&& rm *.zip
	
VOLUME ["/tmp/consul"]
EXPOSE 8500 8600 8400 8301 8302
CMD ["consul", "agent", "-server", "-bootstrap-expect 1", "-data-dir /tmp/consul", "-ui-dir /root/dist"]
