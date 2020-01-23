FROM ubuntu:latest
LABEL maintainer="first087@gmail.com"

RUN apt-get update \
    && apt-get install wget -y \
    && rm -rf /var/lib/apt/lists/* \
    && wget https://minergate.com/download/deb-cli -O install.deb \
    && dpkg -i install.deb \
    && rm -f install.deb \
    && apt-get remove wget -y

ENTRYPOINT [ "minergate-cli" ]

CMD [ "-user", "first087@gmail.com", "-xmr", "2" ]
