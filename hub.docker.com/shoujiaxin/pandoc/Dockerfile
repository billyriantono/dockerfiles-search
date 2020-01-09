FROM alpine:latest

RUN wget https://github.com/jgm/pandoc/releases/download/2.7.3/pandoc-2.7.3-linux.tar.gz \
    && tar xvzf pandoc-2.7.3-linux.tar.gz --strip-components 1 -C /usr/local/ \
    && rm pandoc-2.7.3-linux.tar.gz
