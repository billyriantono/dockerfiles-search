FROM  eclipse-mosquitto AS auth-plugin-builder
RUN apk --no-cache add alpine-sdk curl-dev openssl-dev mosquitto-dev && \
    git clone https://github.com/jpmens/mosquitto-auth-plug.git /plugin && \
    cd /plugin  && \
    cp config.mk.in config.mk && \
    sed -i -- 's/?= yes/?= no/g' config.mk && \
    sed -i -- 's/BACKEND_HTTP ?= no/BACKEND_HTTP ?= yes/' config.mk && \
    make && \
    mkdir -p /mosquitto/lib && \
    cp ./auth-plug.so /mosquitto/lib && \
    cd /mosquitto/lib && \
    rm -rf /plugin

FROM  eclipse-mosquitto
COPY --from=auth-plugin-builder /mosquitto/lib/auth-plug.so /usr/lib
RUN apk --no-cache add libcurl openssl
