# image for building couchberry frontend
# Based on the Fedora image
FROM fedora

# File Author / Maintainer
MAINTAINER Tomas Hozza <thozza@gmail.com>

# image labels
LABEL version="0.3"
LABEL description="image for building couchberry frontend"

# Environment variables
ENV USER user
ENV HOMEDIR /home/${USER}
ENV BUILDDIR ${HOMEDIR}/build
ENV SRCDIR ${HOMEDIR}/sources

# update the system and install build dependencies
RUN \
    dnf -y install \
        nodejs \
        curl \
        which \
        git \
        tar \
        bzip2 \
&& \
    dnf clean all

# we need npm > 2.0.0 due to https://github.com/npm/npm/issues/6043
RUN curl -L https://npmjs.org/install.sh | sh
RUN npm install -g n grunt-cli
# this installs OLD npm!
RUN n 0.10.40 && rm -f /usr/local/bin/npm
RUN npm cache clean -f

# add user used for building the app
RUN useradd -m -d ${HOMEDIR} -m ${USER}

# install dependencies using bower
COPY bower.json ${HOMEDIR}/
COPY package.json ${HOMEDIR}/
RUN chown ${USER}:${USER} ${HOMEDIR}/*.json

# this may not be needed
RUN echo "umask 0000" >> /etc/profile
RUN echo "umask 0000" >> /etc/bashrc

USER ${USER}
RUN umask 0000
WORKDIR ${HOMEDIR}
RUN mkdir ${BUILDDIR}
RUN mkdir ${SRCDIR}

RUN npm install
RUN $(npm bin)/bower install
RUN npm cache clean -f

# make sure any user can read/write/execute the /home/user/*
RUN chmod -R go+rwx ${HOMEDIR}

# directories mounted to image
VOLUME ${BUILDDIR} ${SRCDIR}

# Default entry point
COPY build.sh /usr/bin/build
ENTRYPOINT build

