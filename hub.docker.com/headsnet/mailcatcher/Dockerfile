FROM alpine:3.8

MAINTAINER Ben Roberts <ben@headsnet.com>

RUN apk --no-cache add \
		g++ \
		make \
	    ruby \
	    ruby-dev \
	    sqlite-dev

RUN gem install --no-ri --no-rdoc --conservative etc json mailcatcher

EXPOSE 1080 1025

ENTRYPOINT ["mailcatcher"]
CMD ["--smtp-ip=0.0.0.0", "--http-ip=0.0.0.0", "--foreground"]

