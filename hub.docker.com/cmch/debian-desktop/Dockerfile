
FROM cmch/debian-desktop:docker AS nvidia

ARG DEBIAN_FRONTEND=noninteractive

RUN \
    add-apt-repository \
    "deb http://httpredir.debian.org/debian/ buster main contrib non-free" && \
    apt update && apt install -yq \
    linux-headers-amd64 \
    nvidia-legacy-390xx-driver \
    && apt clean
