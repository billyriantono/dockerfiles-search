FROM noway56/myubuntu
MAINTAINER Lu Wu "wulu@nuanxin-health.com"
LABEL author="Lu Wu"

WORKDIR /workspace

RUN add-apt-repository ppa:ubuntu-desktop/ubuntu-make \
    && add-apt-repository ppa:jonathonf/python-3.6 \
    && apt clean \
    && apt update --fix-missing \
    && apt install -y ubuntu-make python3.6 python3.6-dev \
    && update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1 \
    && update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2 \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3 150 \
    && cp /usr/lib/python3/dist-packages/apt_pkg.cpython-35m-x86_64-linux-gnu.so /usr/lib/python3/dist-packages/apt_pkg.cpython-36m-x86_64-linux-gnu.so \
    && wget https://bootstrap.pypa.io/get-pip.py \
    && python get-pip.py

RUN rm -rfv /var/lib/apt/lists/* && \
    apt clean &&\
    apt autoremove
# CMD ["docker-entrypoint.sh"]
