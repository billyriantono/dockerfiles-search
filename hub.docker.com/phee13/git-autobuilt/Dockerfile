FROM alpine:latest

LABEL version='1.0'
LABEL description='Container image for reversing'

USER root

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN apk update && apk add \
	curl \
	file \
	swig \  
	flex \  
	bison \  
	git \  
	gcc \  
	g++ \  	
	make \  
	glib \ 
	glib-dev \  
	valgrind \  
	gdb \
	yara \
	bash

RUN addgroup -S  user && \
	adduser -D -G  user -h /home/user -s /sbin/nologin  user && \  
	chown -R user:user /home/user

ENV VALA_TAR=vala-0.26.1

WORKDIR /opt

RUN curl -SL https://download.gnome.org/sources/vala/0.26/${VALA_TAR}.tar.xz |   tar -JxC . && \
	cd ${VALA_TAR}; ./configure --prefix=/usr && \  
	make && \
	make install && \  
	cd .. && \  
	rm -rf ${VALA_TAR} && \
	git clone https://github.com/radare/radare2.git && \
	cd radare2 && \  
	./sys/install.sh && \   
	mkdir /home/user/workdir && \  
	chown user:user /home/user/workdir

USER user

RUN r2pm init && \
	r2pm -i r2dec

WORKDIR /home/user/workdir

CMD ["r2"]

