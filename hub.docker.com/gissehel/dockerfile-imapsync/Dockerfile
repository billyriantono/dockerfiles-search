FROM ubuntu:trusty
MAINTAINER Gissehel <public-dockerfile-imapsync@gissehel.org>

# Fetch imapsync source &&
# Install dependencies &&
# Build it
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get -y install build-essential git \
                        makepasswd rcs perl-doc libmail-imapclient-perl libdigest-hmac-perl libterm-readkey-perl libio-socket-ssl-perl libdate-manip-perl \
                        libmail-imapclient-perl libfile-copy-recursive-perl libio-tee-perl libunicode-string-perl && \
    git clone git://github.com/imapsync/imapsync.git && \
    mkdir -p imapsync/dist && \
    cd imapsync && \
    make install

# Define Entrypoint
ENTRYPOINT ["imapsync"]
