FROM ubuntu:latest

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:ubuntu-sdk-team/ppa && \
    add-apt-repository ppa:phablet-team/tools && \
    add-apt-repository ppa:snappy-dev/tools
RUN apt-get update && apt-get install -y mplayer ubuntu-device-flash phablet-tools && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/MariusQuabeck/magic-device-tool.git /magic-device-tool
RUN ubuntu-device-flash --download-only --server=http://system-image.ubports.com touch --channel=ubports-touch/legacy --device=hammerhead 

CMD ["/magic-device-tool/launcher.sh"]
	
		

