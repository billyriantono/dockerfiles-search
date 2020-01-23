FROM ubuntu:16.04
MAINTAINER Christian Hoffmeister <mail@choffmeister.de>

RUN apt-get update && apt-get install --yes makepasswd rcs perl-doc libio-tee-perl git libmail-imapclient-perl libdigest-md5-file-perl libterm-readkey-perl libfile-copy-recursive-perl build-essential make automake libunicode-string-perl libauthen-ntlm-perl libcrypt-ssleay-perl libdigest-hmac-perl libfile-copy-recursive-perl libio-compress-perl libio-socket-inet6-perl libio-socket-ssl-perl libio-tee-perl libmodule-scandeps-perl libnet-ssleay-perl libpar-packer-perl libreadonly-perl libterm-readkey-perl libtest-pod-perl libtest-simple-perl libunicode-string-perl liburi-perl cpanminus && apt-get clean
RUN cpanm JSON::WebToken Test::MockObject Unicode::String Data::Uniqid

WORKDIR /opt/imapsync
RUN git clone git://github.com/imapsync/imapsync.git /opt/imapsync
RUN mkdir dist && make install

ENTRYPOINT ["/usr/bin/imapsync"]
