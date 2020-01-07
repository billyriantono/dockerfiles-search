FROM python:3.6.6-jessie
LABEL maintainer="Larry SU <larry_su@migocorp.com>"

RUN apt-get update \
    && apt-get -y --no-install-recommends install vim \
    && apt-get -y --no-install-recommends install netcat \
    && apt-get -y --no-install-recommends install net-tools

RUN cd ~ \
    && curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh \
    && bash nodesource_setup.sh \
    && rm nodesource_setup.sh \
    && apt-get -y --no-install-recommends install nodejs \
    && apt-get -y --no-install-recommends install build-essential

ENTRYPOINT [ "/bin/bash" ]
