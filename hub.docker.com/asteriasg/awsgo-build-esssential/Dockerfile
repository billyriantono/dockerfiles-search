# for developer
# $ docker build -t awsgo-build-esssential .
# $ docker run -itd -v $PWD:/root/work awsgo-build-esssential
FROM ubuntu:18.04

ARG GOVERSION="1.13.3"
ARG GODOWNLOADFILE="go${GOVERSION}.linux-amd64.tar.gz"

WORKDIR /root

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Tokyo
# these environment are needed to run sam
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

RUN apt update && apt install -y --no-install-recommends \
	tzdata apt-utils ca-certificates make vim less zip unzip curl python3 python3-distutils git jq \
	&& apt clean && rm -rf /var/lib/apt/lists/* && \
	curl -sS -kL https://bootstrap.pypa.io/get-pip.py | python3 && \
	pip3 install awscli aws-sam-cli --upgrade && \
	curl -sS https://dl.google.com/go/${GODOWNLOADFILE} -O && tar -C /usr/local -xzf ${GODOWNLOADFILE} && rm ${GODOWNLOADFILE}
ENV PATH=$PATH:/usr/local/go/bin

CMD ["/bin/bash"]
