FROM ubuntu:xenial
MAINTAINER Andrew Scott <andrew.mark.scott@gmail.com>
LABEL repo="https://github.com/scotta/docker"
LABEL homepage="http://imapsync.lamiral.info/"
LABEL source="https://github.com/imapsync/imapsync"
LABEL description="Imapsync is an IMAP transfer tool. The purpose of imapsync \
is to migrate IMAP accounts or to backup IMAP accounts"
RUN apt-get -y update && apt-get install -y \
    wget unzip make \
    libmail-imapclient-perl \
    libfile-copy-recursive-perl \
    libio-tee-perl \
    libterm-readkey-perl \ 
    libauthen-ntlm-perl \
    libdata-uniqid-perl \
    libio-socket-inet6-perl \
    liburi-perl \
    libtest-pod-perl \
    libunicode-string-perl
RUN wget https://github.com/imapsync/imapsync/archive/master.zip && \
    unzip master.zip
WORKDIR imapsync-master
RUN make install
ENTRYPOINT ["/usr/bin/imapsync", "--noreleasecheck"]
