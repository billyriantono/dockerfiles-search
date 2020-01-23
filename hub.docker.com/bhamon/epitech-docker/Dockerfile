FROM opensuse:13.2
MAINTAINER Benoit Hamon <benoit.hamon@epitech.eu>

RUN zypper --gpg-auto-import-keys -n update
RUN zypper -n install \
    gcc gcc-c++       \
    libX11-devel      \
    libXext-devel     \
    make              \
    which             \
    tar               \
    ksh               \
    tcsh              \
    zsh               \
    ltrace            \
    git               \
    cmake             \
    nasm                       \
    cunit-devel                \
    libSDL-devel libSDL2-devel \
    ncurses ncurses-devel      \
    gmp-devel                  \
    terminfo                   \
    boost-devel                \
    php5                       \
    php5-bcmath                \
    php5-mbstring              \
    python-numpy               \
    python3                    \
    python3-pip                \
    ca-certificates-mozilla    \
    python3-numpy              \
    ruby                       \
    openssh                    \
    ocaml                      \
    ocaml-camlp4      \
    bc                \
    tmux              \
    valgrind gdb      \
    zip unzip         \
    glibc-locale

RUN git clone https://git.cryptomilk.org/projects/cmocka.git/ && \
    cd cmocka                                                 && \
    mkdir build                                               && \
    cd build                                                  && \
    cmake ..                                                  && \
    make                                                      && \
    make install

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN useradd -md /home/mouli mouli
USER mouli

ENV USER mouli

WORKDIR /home/mouli/
