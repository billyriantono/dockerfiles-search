FROM python:2-alpine
MAINTAINER mozster <moz@mozster.net>

ENV GID=991 UID=991

RUN apk add --no-cache openssl

RUN wget -qO- http://github.com/freeranger/evologger/archive/master.tar.gz | tar zxf -

WORKDIR /evologger-master

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

VOLUME /config /output

CMD [ "python", "./evologger.py" ]
