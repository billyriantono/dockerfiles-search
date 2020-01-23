# gotchas/pharo70x64
FROM gotchas/pharo-base64
#FROM gotchas/pharo-base64-vnc
MAINTAINER CAs

#ENV http_proxy ${http_proxy}

ADD *.conf /etc/security/limits.d/

#Setup user and permissions
RUN chgrp -R 0 /opt && \
    chmod -R g=u /opt && \
	chmod g+s /opt
#TEMP
#RUN apt-get update && apt-get install nano

WORKDIR /opt
# Note: this file needs to have Linux End-of-line (LF)
ADD pharo-run .
#RUN ls -la
RUN chmod ug+x pharo-run
	
RUN adduser --disabled-password --gid 0 --gecos "MyUser" myuser
USER myuser
WORKDIR /opt
ENV HOME=/opt

#RUN curl get.pharo.org/64/70+vmI | bash
RUN  umask 0002 &&\
	curl get.pharo.org/64/70+vmT | bash

ADD ./*.st ./
RUN ls -la
RUN ./pharo-run --version
RUN ./pharo-run st --save --quit ./CAs-ProxyEnv.st
RUN ./pharo-run --version
RUN ls -la
#RUN chmod -R g=u Pharo* pharo*
RUN echo "Pharo installed"
