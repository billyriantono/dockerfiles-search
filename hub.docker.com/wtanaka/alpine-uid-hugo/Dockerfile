FROM wtanaka/alpine-37-uid
MAINTAINER http://wtanaka.com/dockerfiles
EXPOSE 1313
ENV HUGO_VERSION 0.53
ENV HUGO_BINARY hugo_${HUGO_VERSION}_linux-64bit
ENV HUGO_DONWLOAD_LOCATION /usr/local/hugo/hugo-bin.tar.gz

# Download and Install hugo
RUN mkdir /usr/local/hugo
ADD https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/${HUGO_BINARY}.tar.gz ${HUGO_DONWLOAD_LOCATION}
RUN tar xzf ${HUGO_DONWLOAD_LOCATION} -C /usr/local/hugo/ \
	&& ln -s /usr/local/hugo/hugo /usr/local/bin/hugo \
	&& rm ${HUGO_DONWLOAD_LOCATION}
