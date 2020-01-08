FROM mrbolae/cpp-cmake-qt-toolchain
MAINTAINER mrbolae <michael.burkard@gmx.ch>

USER root

# update
RUN apt-get update

# install ide
RUN apt-get install -y qtcreator

USER developer

CMD /bin/bash

