FROM clojure:lein-2.8.1-alpine
LABEL maintainer="b.m.lisiecki@gmail.com"

RUN adduser -D clj && \
    mkdir /home/clj/bin
RUN mkdir /app && chown clj:clj /app
WORKDIR /app
USER clj
