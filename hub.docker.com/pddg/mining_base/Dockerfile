FROM python:3.7.0-alpine3.8

LABEL maintainer="Shoma Kokuryo <s.kokuryo@gmail.com>"

# Declare Project dir
ENV PROJECT_DIR /opt/proj

# Change current directory
WORKDIR ${PROJECT_DIR}

# Install dependencies
RUN apk update && \
    # Install build dependencies
    # --virtual=build_dep means that make group as its name 'build_dep'
    apk add --no-cache --virtual=build_dep \
        build-base \
        linux-headers \
        gcc && \
    # Install git for GitPython
    apk add --no-cache \
        libpng-dev \
        freetype-dev \
        git && \
    # Install python modules with pip
    pip3 install --no-cache-dir \
        # http client module
        requests==2.20.1\
        # Manage git repository
        GitPython==2.1.11 \
        # Progress bar module
        tqdm==4.28.1 \
        # Parallel computing
        joblib==0.13.0 \
        # 2D plotting library
        matplotlib==3.0.2 && \
    # Uninstall unnecessary packages
    apk del --purge build_dep

