#########
# container for downloading and extracting the source
#########
FROM alpine:3.8 as builder

WORKDIR /tmp

RUN apk add curl

# download and extract
RUN curl -L -o cmsimple.zip https://www.cmsimple.org/downloadcounter/dlcount/count.php?id=31
RUN unzip cmsimple.zip

# we don't know the exact version number that the extracted folder name contains
RUN mkdir cmsimple
RUN mv CMSimple_*/* cmsimple

#########
# container for demo installation
#########
FROM php:7.2-apache as demo

# copy extracted source and set owner to www-data
COPY --from=builder /tmp/cmsimple .
RUN chown -R www-data:www-data .
