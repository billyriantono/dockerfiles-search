FROM alpine
LABEL maintainer "@flemay"

# update system and install packages
RUN apk --no-cache update && apk --no-cache upgrade \
    && apk --no-cache add --upgrade ca-certificates

# install netlifyctl tool
WORKDIR /opt/netlifyctl
RUN wget -qO- 'https://cli.netlify.com/download/latest/linux' | tar xz
ENV PATH "/opt/netlifyctl:${PATH}"

WORKDIR /opt/app