FROM ubuntu:14.04
MAINTAINER Robert Simmons <robert@simmons.org>

RUN apt-get update && apt-get install -y git python-pip python-dev libxml2-dev libxslt-dev zlib1g-dev

WORKDIR /opt
RUN git clone https://github.com/wyscan/infoq-downloader.git
WORKDIR /opt/infoq-downloader
RUN pip install -r /opt/infoq-downloader/requirements.txt
VOLUME ["/data"]
RUN ln -s /data /opt/infoq-downloader/downloads

ENTRYPOINT ["python", "/opt/infoq-downloader/infoq_downloader.py"]
