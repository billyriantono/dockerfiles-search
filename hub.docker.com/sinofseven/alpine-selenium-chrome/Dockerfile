FROM alpine:edge

RUN apk --no-cache add ruby ruby-json chromium chromium-chromedriver && \
    apk --no-cache add --virtual=build-deps gcc make libc-dev ruby-dev libffi-dev && \
    gem install -N selenium-webdriver && \
    apk del build-deps

CMD ["/bin/sh", "-c", "sh"]
