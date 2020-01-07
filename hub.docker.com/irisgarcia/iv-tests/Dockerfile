FROM perl:5.24-slim-threaded
LABEL version="1.3" maintainer="Iris Garcia <iris.garcia.desebastian@gmail.com>" perl5version="5.28"

ENV SRC_REPO https://github.com/JJ/IV-19-20.git
ENV BRANCH master

# Set up dir and download modules
RUN mkdir /test && apt-get update && \
	apt-get install -y git curl libio-socket-ssl-perl libnet-ssleay-perl && \
	cpanm Test::More Test::Harness Git File::Slurper JSON Net::Ping TAP::Formatter::Color \
	Term::ANSIColor Mojo::UserAgent

WORKDIR /test

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT /entrypoint.sh
