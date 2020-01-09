FROM atlassian/default-image:2

RUN apt-get update \
    && apt-get install apt-transport-https ca-certificates  -y \
    && apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 9DC858229FC7DD38854AE2D88D81803C0EBFCD88 \
    && echo "" > /etc/apt/sources.list.d/docker.list \
    && echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable" >> /etc/apt/sources.list.d/docker.list \
    && apt-get update \
    && apt-get install docker-ce -y \
    && wget https://bootstrap.pypa.io/get-pip.py && python get-pip.py \
    && pip install docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
    && docker --version \
    && docker-compose --version

