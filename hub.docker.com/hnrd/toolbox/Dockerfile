FROM alpine

RUN apk add --no-cache \
  ansible \
  bash \
  coreutils \
  curl \
  git \
  gnupg \
  make \
  openssh \
  socat \
  sudo \
  tree \
  vim \
  zsh
RUN git clone https://git.zx2c4.com/password-store && \
  cd password-store && \
  make install && cd .. && \
  rm -rf password-store
WORKDIR /root
ADD zshrc /root/.zshrc
RUN addgroup user -g 1000 && \
  adduser user -G user -u 1000 -D -s /bin/zsh && \
  cp /root/.zshrc /home/user/.zshrc
ENV LANG=en_US.UTF-8 LC_CTYPE=en_US.UTF-8
CMD zsh
