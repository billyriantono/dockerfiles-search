FROM alpine:latest

# Hugo Versions
ENV HUGO_VERSION 0.62.0
ENV HUGO_CHECKSUM a13e830b8dd6b3ad3948f59ea395c4592e8ca0c05a950af29c6db5291423f467

# Container Annotations based on https://github.com/opencontainers/image-spec/blob/master/annotations.md
ARG IMAGE_REVISION=1
ARG IMAGE_BUILD_TIME
LABEL org.opencontainers.image.authors="@m4rcs" \
      org.opencontainers.image.created="${IMAGE_BUILD_TIME}" \
      org.opencontainers.image.description="The world’s fastest framework for building websites."\
      org.opencontainers.image.documentation="https://github.com/m4rcs/docker-hugo" \
      org.opencontainers.image.licenses="Apache-2.0" \
      org.opencontainers.image.revision="${IMAGE_REVISION}" \
      org.opencontainers.image.source="https://github.com/m4rcs/docker-hugo.git" \
      org.opencontainers.image.title="Docker Hugo" \
      org.opencontainers.image.url="https://github.com/m4rcs/docker-hugo" \
      org.opencontainers.image.vendor="GoHugo.io" \
      org.opencontainers.image.version="v${HUGO_VERSION}"

# Download required files and packages, check them and install hugo into the path
WORKDIR /tmp
RUN apk add --no-cache ca-certificates libc6-compat libstdc++ && \
    wget -q https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_Linux-64bit.tar.gz && \
    echo "${HUGO_CHECKSUM}  hugo_extended_${HUGO_VERSION}_Linux-64bit.tar.gz" | sha256sum -cs - && \
    tar xfz hugo_extended_${HUGO_VERSION}_Linux-64bit.tar.gz && \
    mv /tmp/hugo /usr/bin && \
    rm -rf /tmp/* && \
    mkdir /site

# Put the source of your site into /site
WORKDIR /site
VOLUME [ "/site" ]
EXPOSE 1313

# Run hugo
CMD [ "/usr/bin/hugo" ]
