FROM pigiuz/docker-virtualgl
RUN apt-get update -y && \
    apt-get install software-properties-common python-software-properties -y && \
    add-apt-repository ppa:ubuntu-mozilla-security/ppa -y && \
    apt-get update -y && \
    apt-get install firefox -y
ENTRYPOINT vglrun firefox
