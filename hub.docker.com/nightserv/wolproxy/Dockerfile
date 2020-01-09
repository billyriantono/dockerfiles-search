FROM alpine:latest

RUN apk update
RUN apk add python3 
RUN pip3 install wakeonlan

COPY wolproxy.py /opt/
EXPOSE 8080

ENTRYPOINT python3 -u /opt/wolproxy.py
