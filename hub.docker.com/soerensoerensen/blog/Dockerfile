FROM nginx:stable-alpine

ENV HUGO_VERSION 0.40.3
ENV HUGO_BINARY hugo_${HUGO_VERSION}_linux-64bit

COPY src /tmp/blog

ADD https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/${HUGO_BINARY}.tar.gz /tmp/

RUN ls /tmp
RUN mkdir -p /opt/hugo \
    && tar xzf /tmp/${HUGO_BINARY}.tar.gz -C /opt/hugo/ \
    && ln -s /opt/hugo/hugo /usr/local/bin/hugo \
    && rm /tmp/${HUGO_BINARY}.tar.gz

RUN hugo -s /tmp/blog --destination /usr/share/nginx/html \
    && rm -rf /tmp/blog
