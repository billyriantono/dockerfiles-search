#
# Python image
#

FROM 1science/alpine:3.5

# Python Version
ENV PYTHON_VERSION=2.7.13-r0

# Install build-base (build-essential equivalent), and Python 2.7
RUN apk add ncurses-dev build-base
RUN apk add "python=${PYTHON_VERSION}" "python-dev=${PYTHON_VERSION}" && \
    curl -LS "https://bootstrap.pypa.io/get-pip.py" | python && \
    pip install virtualenv && \
    echo -ne "- with `python --version 2>&1`\n" >> /root/.built
