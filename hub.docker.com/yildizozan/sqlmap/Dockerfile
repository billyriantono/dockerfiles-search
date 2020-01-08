FROM python:3.7.6-alpine3.10

LABEL maintainer="Ozan Yıldız <developer@yildizozan>"

RUN wget -O /sqlmap.tar.gz https://github.com/sqlmapproject/sqlmap/archive/1.4.tar.gz

RUN tar -zxvf sqlmap.tar.gz

ENTRYPOINT ["python", "/sqlmap-1.4/sqlmap.py"]

CMD ["-h"]
