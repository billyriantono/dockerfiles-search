FROM almir/webhook

LABEL author=opiskull

ENV HUGO_VERSION=0.38.2
ADD https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz /tmp
RUN tar -xf /tmp/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz -C /tmp \
    && mkdir -p /usr/local/sbin \
    && mv /tmp/hugo /usr/local/sbin/hugo \
    && rm -rf /tmp

RUN apk add --update --no-cache git bash \
    && apk upgrade \
    && apk add --no-cache ca-certificates

EXPOSE 9000

VOLUME [ "/hooks", "/output", "/src" ]

ENTRYPOINT [ "/usr/local/bin/webhook", "-hooks=/hooks/hooks.yaml.tmpl", "-template", "-hotreload", "-verbose"]