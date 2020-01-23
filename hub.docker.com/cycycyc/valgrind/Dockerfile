FROM ubuntu
WORKDIR /root

RUN apt-get update -yq \
    && apt-get install -y --no-install-recommends make g++ yasm nasm cmake-curses-gui valgrind \
    && rm -rf /var/lib/apt/lists/*