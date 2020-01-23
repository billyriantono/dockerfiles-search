FROM python:3-alpine
MAINTAINER	DACRepair  <DACRepair@gmail.com>

WORKDIR /usr/src/app

ENV UDPPORT 5005
COPY udplistener.py /usr/src/app/udplistener.py

EXPOSE ${UDPPORT}
EXPOSE ${UDPPORT}/udp

CMD ["python", "-u","udplistener.py"]
