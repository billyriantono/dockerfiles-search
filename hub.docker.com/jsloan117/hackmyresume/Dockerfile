FROM alpine:latest
LABEL Name=hackmyresume Version=1.1
LABEL maintainer="Jonathan Sloan"

RUN echo "*** updating system ***" \
    && apk update && apk upgrade \
    && echo "*** installing packages ***" \
    && apk --no-cache add bash wkhtmltopdf nodejs npm \
    && echo "*** cleanup ***" \
    && rm -rf /tmp/* /var/tmp/*

RUN npm install -g \
    hackmyresume \
    jsonresume-theme-eloquent \
    jsonresume-theme-elegant \
    jsonresume-theme-paper \
    jsonresume-theme-kendall \
    jsonresume-theme-modern \
    jsonresume-theme-classy \
    jsonresume-theme-class \
    jsonresume-theme-short \
    jsonresume-theme-slick \
    jsonresume-theme-kwan \
    jsonresume-theme-onepage \
    jsonresume-theme-spartan \
    jsonresume-theme-stackoverflow
