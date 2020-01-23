FROM alpine:3.10.1 as build

# set curl version
# for hand testing: export CURLVERSION=curl-7.65.3
ENV CURLVERSION curl-7.65.3

# compile stand-alone curl from source
RUN apk add --no-cache openssl-dev wget build-base \
    && wget https://curl.haxx.se/download/$CURLVERSION.tar.gz \
    && tar xvzf $CURLVERSION.tar.gz \
    && rm $CURLVERSION.tar.gz \
    && cd $CURLVERSION \
    && ./configure --with-ca-fallback --disable-shared \
    && make curl_LDFLAGS=-all-static \
    && make install

# use busybox for a smaller, simple, entrypoint for scripting
FROM busybox:1.31.0

# copy stand-alone compiled curl to bash container
COPY --from=build /usr/local/bin/curl /usr/local/bin/curl

# TO BUILD:
# docker build --no-cache -t tinycurl:latest .
# TO TEST:
# docker run -it tinycurl:latest
# TO SCRIPT:
# docker run -it tinycurl:latest /usr/local/bin/bash -c "cd var/; ls; echo 'hello'; curl -L google.com; echo 'done'"
