FROM debian:jessie
MAINTAINER jamie.woods@bbc.co.uk

RUN apt-get update && apt-get install -y \
  libmoose-perl liburi-perl libmoosex-getopt-perl libsocket6-perl libanyevent-perl cpanminus build-essential

RUN mkdir -p /app
WORKDIR /app

RUN cpanm --quiet --notest AnyEvent::MPRPC::Client

COPY . ./

RUN perl Makefile.PL && make && make test && make install

CMD ["sh", "-c", "./rtsp-server.pl"]
