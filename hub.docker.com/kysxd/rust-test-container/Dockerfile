FROM rust:latest

RUN apt-get update -yq
RUN rustup component add rustfmt
RUN apt-get install -y \
    alsa-utils \
    libasound2-dev \
    cmake \
    git \
    libasound2-dev \
    libx11-xcb-dev \
    libssl-dev cmake \
    libfreetype6-dev \
    libexpat1-dev \
    libxcb1-dev \
    python3 \
    build-essential \
    libsdl2-dev

CMD ["bash"]
