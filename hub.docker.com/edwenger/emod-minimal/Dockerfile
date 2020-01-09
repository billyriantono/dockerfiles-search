FROM ubuntu:18.04

ENV USER=luser
ENV PATH=$PATH:/usr/lib64/mpich/bin

RUN apt-get update && apt-get install -y \
	openmpi-bin \
	python3-dev \
	ssh

COPY bin/Eradication /bin/
RUN chmod +x /bin/Eradication
