FROM ubuntu:16.04

RUN useradd 'hab' --system \
    && apt update \
    && apt install --yes 'curl' 'bash' \
    && apt clean \
    && apt autoremove \
    && curl --silent 'https://raw.githubusercontent.com/habitat-sh/habitat/master/components/hab/install.sh' | bash \
    && hab pkg install 'core/hab-launcher' \
    && hab pkg install 'core/hab-sup'
