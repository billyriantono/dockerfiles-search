FROM ubuntu:14.04
ENV USER root

RUN apt-get update && apt-get install -y \
	autotools-dev \
	debhelper \
	dpatch \
	gdb \
	libc6-dev \
	gcc-multilib \
	libc6-dbg \
	valgrind
	
COPY lang /opt/
COPY startvalgrind.sh /opt/
RUN  chmod +x /opt/startvalgrind.sh
ENTRYPOINT ["/opt/startvalgrind.sh"]
