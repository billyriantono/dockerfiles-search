FROM ubuntu:bionic-20180821

ENV GOSU_URL https://github.com/tianon/gosu/releases/download/1.4/gosu

# change sh from, possibly, dash to bash
RUN cd /bin && rm sh && ln -s bash sh

# apt
RUN apt-get update -y

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
	--no-install-recommends apt-utils

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
	vim bash-completion sudo

# creating user with matching host id on the fly magic
RUN echo ""
COPY entrypoint.sh /usr/local/bin/entrypoint.sh

RUN apt-get update -y
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    ca-certificates \
    curl \
    gpg

RUN mkdir ~/.gnupg
RUN echo "disable-ipv6" >> ~/.gnupg/dirmngr.conf
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN curl -o /usr/local/bin/gosu -SL "$GOSU_URL-$(dpkg --print-architecture)"
RUN curl -o /usr/local/bin/gosu.asc -SL "$GOSU_URL-$(dpkg --print-architecture).asc"
RUN gpg --verify /usr/local/bin/gosu.asc
RUN rm /usr/local/bin/gosu.asc
RUN chmod +x /usr/local/bin/gosu
RUN chmod +x /usr/local/bin/entrypoint.sh
# end of creating user with matching host id on the fly magic

# build-essential and other build/make package
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
	build-essential make cmake cmake-curses-gui python3 \
	flex bison automake bc module-init-tools

# nice to have extras
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
	curl wget libspeex-dev sox libogg-dev

# testing extras
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
	socat cppcheck python-pygments

# others
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
	kpartx dosfstools cifs-utils rsync
	
# user setup
#RUN useradd docker -d /home/docker -m -s /bin/bash &&\
# 	passwd -d docker &&\
#	echo "docker  ALL=(ALL)       NOPASSWD: ALL" >> /etc/sudoers; echo "Defaults    !requiretty" >> /etc/sudoers

ENV EXPORT_DIR /export
VOLUME ["$EXPORT_DIR"]
WORKDIR $EXPORT_DIR

#ENTRYPOINT ["tail", "-f", "/dev/null"]
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
