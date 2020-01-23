FROM djx339/buildpack-deps:ubuntu-14.04-sshd
MAINTAINER Dainel D <djx339@gmail.com>

RUN apt-get update && apt-get install -y --no-install-recommends vim \
    && rm -rf /var/lib/apt/lists/* \
    && git clone https://github.com/djx339/dotfiles.git ~/dotfiles \
    && /root/dotfiles/install.sh
