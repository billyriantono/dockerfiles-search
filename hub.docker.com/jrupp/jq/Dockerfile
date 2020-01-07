FROM alpine
LABEL maintainer="Justin Rupp <dither@gmail.com>"
ENV VERSION 1.6
RUN apk add --update curl \
    && curl -o /usr/local/bin/jq -L https://github.com/stedolan/jq/releases/download/jq-$VERSION/jq-linux64 \
    && chmod +x /usr/local/bin/jq
FROM scratch
COPY --from=0 /usr/local/bin/jq /usr/local/bin/jq
ENTRYPOINT ["/usr/local/bin/jq"]
CMD        ["--help"]