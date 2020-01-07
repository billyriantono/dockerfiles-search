FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
	python3.6

RUN adduser --gecos '' --disabled-password pysrv

USER pysrv

RUN mkdir -p /home/pysrv/vscredirect

COPY /src/index.html /home/pysrv/vscredirect/

COPY /src/httpServer.py /home/pysrv/

ENTRYPOINT ["python3.6", "/home/pysrv/httpServer.py" ]

EXPOSE 8444