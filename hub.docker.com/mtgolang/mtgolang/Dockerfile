FROM alpine:3.3
MAINTAINER aerth@sdf.org
ENV GOLANG_VERSION 1.6
ENV GOLANG_SRC_URL https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz
ENV GOLANG_SRC_SHA256 a96cce8ce43a9bf9b2a4c7d470bc7ee0cb00410da815980681c8353218dcf146

ENV GOLANG_BOOTSTRAP_VERSION 1.4.3
ENV GOLANG_BOOTSTRAP_URL https://golang.org/dl/go$GOLANG_BOOTSTRAP_VERSION.src.tar.gz
ENV GOLANG_BOOTSTRAP_SHA1 486db10dc571a55c8d795365070f66d343458c48

RUN set -ex \
	&& apk add --no-cache --virtual .build-deps \
		bash \
		ca-certificates \
		gcc \
		musl-dev \
		openssl \
		git \
	\
	&& mkdir -p /usr/local/bootstrap \
	&& wget -q "$GOLANG_BOOTSTRAP_URL" -O golang.tar.gz \
	&& echo "$GOLANG_BOOTSTRAP_SHA1  golang.tar.gz" | sha1sum -c - \
	&& tar -C /usr/local/bootstrap -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& cd /usr/local/bootstrap/go/src \
	&& ./make.bash \
	&& export GOROOT_BOOTSTRAP=/usr/local/bootstrap/go \
	\
	&& wget -q "$GOLANG_SRC_URL" -O golang.tar.gz \
	&& echo "$GOLANG_SRC_SHA256  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& cd /usr/local/go/src \
	&& ./make.bash \
	\
	&& rm -rf /usr/local/bootstrap /usr/local/go/pkg/bootstrap
RUN wget http://www.archlinux.org/packages/core/i686/glibc/download/ -O glibc.pkg.tar.xz
RUN apk add libgcc
RUN tar xfJ glibc.pkg.tar.xz -C /
ENV PATH $PATH:/home/gopher/go/bin:/usr/local/go/bin:/opt/bin
ENV GOPATH /tmp/mtgolang
ENV GOBIN /opt/bin/
RUN go get -v -u github.com/mtgolang/gobox
RUN gobox -install /opt/bin/
RUN go get github.com/mtgolang/go-coreutils/ln
RUN go get github.com/mtgolang/go-coreutils/whoami
RUN go get github.com/kisielk/vigo
#RUN go get github.com/dborzov/lsp
RUN go get github.com/dacez/lsp
RUN go get github.com/jingweno/ccat
#RUN go get github.com/elves/elvish
RUN go get github.com/dacez/dcd
RUN rm /opt/bin/cat; ln -s /opt/bin/ccat /opt/bin/cat
#RUN rm /opt/bin/ls; ln -s /opt/bin/lsp /opt/bin/ls
RUN ln -s /opt/bin/vigo /opt/bin/vi
RUN ln -s /opt/bin/vigo /opt/bin/vim

RUN apk update
RUN apk add openssh
RUN apk add openrc &&\
# Tell openrc its running inside a container, till now that has meant LXC
    sed -i 's/#rc_sys=""/rc_sys="lxc"/g' /etc/rc.conf &&\
# Tell openrc loopback and net are already there, since docker handles the networking
    echo 'rc_provide="loopback net"' >> /etc/rc.conf &&\
# can't get ttys unless you run the container in privileged mode
    sed -i '/tty/d' /etc/inittab &&\
# can't set hostname since docker sets it
    sed -i 's/hostname $opts/# hostname $opts/g' /etc/init.d/hostname &&\
# can't mount tmpfs since not privileged
    sed -i 's/mount -t tmpfs/# mount -t tmpfs/g' /lib/rc/sh/init.sh &&\
# can't do cgroups
    sed -i 's/cgroup_add_service /# cgroup_add_service /g' /lib/rc/sh/openrc-run.sh
RUN touch /var/log/rc.log
RUN rc-update add sshd
RUN rc-status

RUN touch /run/openrc/softlevel
RUN rc-service sshd restart


RUN cp /usr/bin/git /opt/bin/git








# Workaround lack of copy command
RUN cp /bin/cp /opt/bin/cp


# Installation Complete. Now let's create the user.
RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R +x "$GOPATH/bin"
RUN addgroup gophers
RUN adduser -D gopher -h /home/gopher -H -s /opt/bin/shell -G gophers
RUN mkdir /home/gopher/
RUN mkdir /home/gopher/docs

#ADD https://github.com/aerth.keys /home/gopher/.ssh/authorized_keys
RUN chown -R gopher:gophers /home/gopher

# Remove old busybox
ENV PATH /opt/bin:$PATH
RUN rm /bin/sh && cp /opt/bin/shell /bin/sh
RUN ln -s /opt/bin/shell /opt/bin/sh
RUN chgrp root /sbin /oldbin /usr/bin/ /usr/sbin
RUN chmod o-x /sbin /oldbin /usr/bin/ /usr/sbin

# Clean up
RUN rm /glibc.pkg.tar.xz
RUN mv /bin/ /opt/nbin
RUN mv /usr/sbin /opt/nsbin
RUN rm -Rf /tmp/mtgolang
RUN apk remove openssh-client
RUN apk remove openssh

# Switch to user. Full path *for now*
USER gopher
ENV GOPATH /home/gopher/go
ENV GOBIN /home/gopher/go/bin
ENV PATH /home/gopher/go/bin:/usr/local/go/bin:/opt/bin
#ENV PATH /home/gopher/go/bin:/usr/local/go/bin:/opt/bin:$PATH
WORKDIR /home/gopher
RUN go get -u github.com/mtgolang/mtgolang/cmd/HELP
ADD ./docs/help /opt/bin/help # update
ADD ./docs/chat /opt/bin/chat # update
CMD ["/bin/sh"]

