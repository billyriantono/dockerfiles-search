FROM cybe/ps-base:alpine37

RUN apk --no-cache add --virtual .fetch-deps openssl ca-certificates \
# Fetch emailrelay
    && wget https://sourceforge.net/projects/emailrelay/files/emailrelay/1.9/emailrelay-1.9-src.tar.gz/download -O emailrelay.tar.gz \
    && echo "a0ac885e135a7a53ebb38d22483f37e762f7202c  emailrelay.tar.gz" | sha1sum -c - \
    && tar -xzf emailrelay.tar.gz \
    && cd /emailrelay-* \
# Add build dependencies and remove fetch dependencies
    && apk --no-cache add --virtual .build-deps build-base openssl-dev zlib-dev \
    && apk del --purge .fetch-deps \
# Build and install emailrelay
    && export CXXFLAGS="-g -O2 -Wno-deprecated-declarations" \
    && bin/configure-fhs.sh --disable-testing --disable-install-hook --disable-pop --disable-exec --disable-admin --disable-auth --disable-proxy \
    && make \
    && strip -s src/main/emailrelay src/main/emailrelay-* \
    && make install \
    && cd / \
# Remove unneccesary files
    && rm -rf /usr/lib/emailrelay/examples/ \
    && rm -f /etc/init.d/emailrelay \
    && rm -rf /usr/share/emailrelay \
    && rm -f /etc/emailrelay.* \
    && rm -rf /usr/share/doc/emailrelay \
    && rm -rf /usr/share/man/man1 \
# Cleanup
    && rm /emailrelay.tar.gz \
    && rm -rf /emailrelay-* \
# Add runtime dependencies and remove build dependencies
    && apk add --no-cache openssl libstdc++ \
    && apk del --purge .build-deps

CMD ["emailrelay", "--no-daemon", "--remote-clients", "--client-auth", "/emailrelay/auth", "--client-tls", "--domain", "pinshot.net", "--forward-to", "sslout.df.eu:587", "--poll", "60", "--log-time", "--no-syslog", "--log", "--port", "25", "--response-timeout", "60", "--user", "nobody"]
