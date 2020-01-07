FROM python:2.7.9
MAINTAINER silverbirder <silverbirder@gmail.com>

ENV IP_ADDRESS 127.0.0.1
ENV MESSAGE "HELLO"

WORKDIR /app
COPY main.js package.json services.sh ./
RUN echo "deb http://deb.debian.org/debian jessie main" > /etc/apt/sources.list &&\
    echo "deb http://security.debian.org jessie/updates main" >> /etc/apt/sources.list &&\
    curl -sL https://deb.nodesource.com/setup_8.x | bash - &&\
    apt-get update -qq &&\
    # https://github.com/noelportugal/google-home-notifier#raspberry-pi
    apt-get install -y nodejs libnss-mdns libavahi-compat-libdnssd-dev avahi-daemon &&\
    npm i &&\
    chmod 744 services.sh &&\
    # https://github.com/noelportugal/google-home-notifier#after-npm-install
    sed -i 's/getaddrinfo()/getaddrinfo({families:[4]})/g' node_modules/mdns/lib/browser.js &&\
    # https://github.com/zlargon/google-tts/issues/22
    sed -i -e 's/"google-tts-api": \(.*\)/"google-tts-api": "0.0.4",/g' node_modules/google-home-notifier/package.json &&\
    cd node_modules/google-home-notifier &&\
    npm update google-tts-api &&\
    cd /app

CMD ["/app/services.sh"]