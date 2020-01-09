FROM alpine:edge
LABEL maintainer "smapira@routeflags.com"

# Update Alpine environment
RUN apk add --update --no-cache g++ make build-base ruby-dev libc-dev linux-headers openssl-dev libxml2-dev libxslt-dev ca-certificates

## Install Ruby
ENV RUBY_MAJOUR  2.4
ENV RUBY_VERSION     2.4.1
RUN wget -q "http://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOUR}/ruby-${RUBY_VERSION}.tar.gz" -O ruby-${RUBY_VERSION}.tar.gz
RUN tar zxf ruby-${RUBY_VERSION}.tar.gz
RUN cd ruby-${RUBY_VERSION} && ./configure --disable-install-doc --disable-install-rdoc && make && make install
RUN echo "install: --no-document" > $HOME/.gemrc && echo "update: --no-document" >> $HOME/.gemrc
RUN gem install bundler

CMD ["irb"]
