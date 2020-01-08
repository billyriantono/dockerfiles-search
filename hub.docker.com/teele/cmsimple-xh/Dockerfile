#########
# container for downloading and extracting the source
#########
FROM alpine:3.8 as builder

WORKDIR /tmp

RUN apk add curl

# download and extract
RUN curl -L -o cmsimplexh.zip https://github.com/cmsimple-xh/cmsimple-xh/releases/download/1.7.2/CMSimple_XH-1.7.2.zip
RUN unzip cmsimplexh.zip

#########
# container for demo installation
#########
FROM php:7.2-apache as demo

# copy extracted source and set owner to www-data
COPY --from=builder /tmp/cmsimplexh .
RUN chown -R www-data:www-data .
