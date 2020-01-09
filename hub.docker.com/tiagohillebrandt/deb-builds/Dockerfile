FROM ubuntu:bionic

ENV TZ=America/Chicago

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
        fakeroot \
        git \
        make \
        packaging-dev
