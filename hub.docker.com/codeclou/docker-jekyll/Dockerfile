FROM alpine:3.5

#
# VERSIONS
#
ENV JEKYLL_VERSION 3.3.1

#
# INSTALL BASE PACKAGES
#
RUN apk add --no-cache \
            gcc \
            build-base \
            wget \
            libatomic \
            readline \
            readline-dev \
            libxml2 \
            libxml2-dev \
            ncurses-terminfo-base \
            ncurses-terminfo \
            libxslt \
            libxslt-dev \
            zlib \
            zlib-dev \
            yaml \
            yaml-dev \
            libffi-dev \
            unzip \
            ruby \
            ruby-dev \
            ruby-rdoc \
            ruby-irb \
            ruby-json \
            ruby-bundler \
            ruby-rake \
            ruby-io-console \
            ruby-libs && \
    gem install --no-document  jekyll -v "${JEKYLL_VERSION}" && \
    apk del build-base \
            zlib-dev \
            ruby-dev \
            readline-dev \
            yaml-dev \
            libffi-dev \
            libxml2-dev


#
# PREPARE USER MODE
#
RUN addgroup -g 10777 rubyworker && \
    adduser -D -G rubyworker -u 10777 rubyworker && \
    mkdir -p /rubyapp/ && chown -R rubyworker:root /rubyapp/

#
# VOLUMES AND EXPOSE
#
WORKDIR "/rubyapp/"
VOLUME ["/rubyapp"]
EXPOSE 4000

#
# RUN IN USER MODE
#
USER rubyworker
ENTRYPOINT ["jekyll"]
CMD ["--help"]