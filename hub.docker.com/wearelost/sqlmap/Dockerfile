FROM python:2-alpine

WORKDIR /

RUN wget -O - https://github.com/sqlmapproject/sqlmap/archive/1.3.2.tar.gz  | tar zxf -

ENTRYPOINT ["python", "/sqlmap-1.3.2/sqlmap.py"]
