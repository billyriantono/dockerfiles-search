FROM dock0/arch
MAINTAINER Jon Chen <bsd@voltaire.sh>

ENV GOPATH /opt/go
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/go/bin
RUN mkdir -p /opt/go
RUN /usr/sbin/pacman -Syu go subversion mercurial git bzr --needed --noconfirm
