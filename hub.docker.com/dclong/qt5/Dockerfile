FROM dclong/ubuntu_b

RUN apt-get update -y \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        build-essential libfontconfig1 mesa-common-dev libglu1-mesa-dev qt5-default \
    && apt-get autoremove -y \
    && apt-get autoclean -y

ENTRYPOINT ["/scripts/sys/init.sh"]
