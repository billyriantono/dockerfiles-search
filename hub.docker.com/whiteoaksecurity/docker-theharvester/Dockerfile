FROM alpine:latest
MAINTAINER Christopher Emerson <christopher.emerson@whiteoaksecurity.com>

RUN apk add --update bash git python py-pip && rm -rf /var/cache/apk/*

RUN pip install requests && git clone https://github.com/laramies/theHarvester.git && chmod +x theHarvester/theHarvester.py


RUN mkdir /output
VOLUME ["/output"]
WORKDIR /theHarvester

ENTRYPOINT ["python", "theHarvester.py"]
