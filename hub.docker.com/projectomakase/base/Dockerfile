FROM debian:8

MAINTAINER Richard Lucas <feedback@projectomakase.com>

RUN \
	apt-get update && \		
	apt-get -y install curl && \
	apt-get -y install unzip && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*
	
RUN adduser --system --uid 1001 --home /var/omakase --shell /sbin/nologin --group --debug omakase

WORKDIR /var/omakase

USER omakase

CMD ["bash"]	