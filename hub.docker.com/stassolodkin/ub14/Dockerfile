FROM ubuntu:14.04
MAINTAINER Stas Solodkin <stas.solodkin@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

ARG hostname=ms.solodkins.com
ARG password=3RdInRoot!

RUN touch /etc/init.d/systemd-logind

RUN apt-get update && apt-get install -y \
			openssh-server \
			git \
			tar \
			zip \
			net-tools \
			dnsutils \
			sysstat \
                        openssl \
                        libssl0.9.8 \
			dnsutils \
			curl \
			libcurl3 \
			libcurl3-dev \
			fop \
			software-properties-common \
			python-software-properties

RUN mkdir /var/run/sshd
RUN echo 'root:$password' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
RUN echo "export EDITOR=vi" >> /etc/profile

RUN apt-get update && apt-get -f install

RUN useradd -m -s /bin/bash -G sudo stas
RUN echo 'stas:3RdInRoot!' | chpasswd
