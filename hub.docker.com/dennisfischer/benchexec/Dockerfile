FROM ubuntu:18.04

RUN apt-get update \
	&& apt-get install -y wget python3-setuptools python3-pip python3-tempita \
	&& rm -rf /var/lib/apt/lists/*
RUN wget https://github.com/sosy-lab/benchexec/releases/download/1.16/benchexec_1.16-1_all.deb && dpkg -i benchexec_*.deb && rm benchexec_*.deb
RUN mkdir /app
WORKDIR /app
CMD ["python3", "-m", "benchexec.check_cgroups"]