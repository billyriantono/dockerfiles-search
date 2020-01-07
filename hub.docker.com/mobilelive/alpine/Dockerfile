FROM alpine:latest
MAINTAINER mobilelive/dockerfiles

# install #

ENV PATH /app/bin:$PATH

# setup #

RUN mkdir /app
RUN mkdir /app/bin /app/com /app/etc /app/share /app/var
RUN addgroup -S app
RUN adduser -SH -s /bin/sh -h /app -G app app
RUN chown -R app:app /app
# USER app
WORKDIR /app

# cmd #

CMD [ "sh" ]




