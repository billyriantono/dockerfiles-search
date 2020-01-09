FROM codenvy/cpp_gcc

MAINTAINER Matthias Fuchs <matz.fuchs@gmx.at>

User root

RUN apt-get update \
    && apt-get install -y cmake-curses-gui libboost-all-dev python-dev libzip-dev libxerces-c-dev libopencv-dev libcppunit-dev libgl1-mesa-dev libglew-dev python-pip python-daemon python-opencv \
    && curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get install -y nodejs \
    && pip install tornado \
    && npm install -g ember-cli

User user
