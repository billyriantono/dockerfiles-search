FROM alpine
MAINTAINER Fabrizio Steiner

# Set up certificates and our base tools.
RUN apk --no-cache add \
    ca-certificates \
    openssl \
    curl \
    git \
    git-lfs \
    && git lfs install

RUN apk --no-cache add py-pygments

# Download and install hugo
ENV HUGO_VERSION 0.42.1
ENV HUGO_DOWNLOAD_FILE hugo_${HUGO_VERSION}_Linux-64bit.tar.gz

ADD https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/${HUGO_DOWNLOAD_FILE} /tmp/hugo.tar.gz
RUN tar -xvzf /tmp/hugo.tar.gz -C /tmp/ \
	&& mv /tmp/hugo /usr/bin/hugo && rm -rf /tmp/*

# Create working directory
RUN mkdir /usr/share/blog
WORKDIR /usr/share/blog

# Expose default hugo port
EXPOSE 1313

# Automatically build site
ONBUILD ADD site/ /usr/share/blog
ONBUILD RUN hugo -d /usr/share/nginx/html/

# By default, serve site
ENV HUGO_BASE_URL http://localhost:1313
CMD hugo server -b ${HUGO_BASE_URL} --bind=0.0.0.0
