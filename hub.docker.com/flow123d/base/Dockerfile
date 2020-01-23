FROM ubuntu:16.04
MAINTAINER Jan Hybs
ENV LANG C.UTF-8

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION=1.0
ARG BUILD_TYPE=Debug

LABEL org.label-schema.build-date="$BUILD_DATE" \
      org.label-schema.name="Flow123d" \
      org.label-schema.description="Transport Processes in Fractured Media" \
      org.label-schema.url="http://flow123d.github.io/" \
      org.label-schema.vcs-ref="$VCS_REF" \
      org.label-schema.vcs-url="https://github.com/flow123d/flow123d" \
      org.label-schema.vendor="Technical University of Liberec" \
      org.label-schema.version="$VERSION" \
org.label-schema.schema-version="1.0"

RUN apt-get update && apt-get install -y \
    sudo \
    make \
    wget  \
    python3 \
    bash-completion \
    apt-utils \
    nano \
    less \
    man \
    ca-certificates \
    curl \
    gosu \
&& rm -rf /var/lib/apt/lists/*

# copy entrypoint script
COPY entrypoint.sh /usr/local/bin/entrypoint.sh

# install mpich
RUN wget -qO /tmp/mpich-3.2.0.deb "http://ciflow.nti.tul.cz/static/packages/mpich_3.2.0_$BUILD_TYPE/mpich-3.2.0.deb" \
 && dpkg -i /tmp/mpich-3.2.0.deb \
 && rm -rf /tmp/*.deb

# edit env variables so mpich can be found
ENV MPICH_DIR="/usr/local/mpich-3.2.0" \
    PATH="/usr/local/mpich-3.2.0/bin:$PATH" \
    LIBRARY_PATH="/usr/local/mpich-3.2.0/lib:$LIBRARY_PATH" \
    LD_LIBRARY_PATH="/usr/local/mpich-3.2.0/lib:$LD_LIBRARY_PATH" \
    MANPATH="/usr/local/mpich-3.2.0/share/man:$MANPATH"


# save the image version
RUN echo "base" > /.dockerversion

# set entrypoint script
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
# and default argument
CMD ["/bin/bash"]

