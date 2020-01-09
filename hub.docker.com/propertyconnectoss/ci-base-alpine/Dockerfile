FROM circleci/node:8

ENV BUILD_SCRIPTS   /build-scripts

ENV PATH            ${BUILD_SCRIPTS}:$PATH

RUN sudo mkdir -p ${BUILD_SCRIPTS}
ADD build-scripts ${BUILD_SCRIPTS}

RUN sudo npm install -g npm