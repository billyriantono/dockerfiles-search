FROM konmeo/minideb

MAINTAINER konmeo

WORKDIR /workdir

RUN install_packages build-essential git wget

ENV CPPFLAGS='-pipe' \
    MAKEFLAGS='-j$(($(nproc)+1))'

RUN git config --global http.followRedirects true
