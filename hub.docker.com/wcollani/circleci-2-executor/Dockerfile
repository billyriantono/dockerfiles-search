FROM bitnami/minideb:jessie

LABEL maintainer="wcollani@gmail.com" \
      version="v0.1.0"

RUN install_packages git ssh tar gzip unzip ca-certificates \
	 apt-transport-https curl python-software-properties wget

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
	 echo "deb [arch=amd64] https://download.docker.com/linux/debian jessie stable" >> /etc/apt/sources.list


RUN install_packages docker-ce

RUN wget https://github.com/tcnksm/ghr/releases/download/v0.5.4/ghr_v0.5.4_linux_amd64.zip && \
	 unzip ghr_v0.5.4_linux_amd64.zip && rm ghr_v0.5.4_linux_amd64.zip && \
	 mv /ghr /usr/local/bin/ghr
