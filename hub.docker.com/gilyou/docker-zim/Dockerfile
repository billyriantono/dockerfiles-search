FROM ubuntu:bionic
LABEL org.label-schema.build-date=$BUILD_DATE \
      maintainer="Renwu Gao <gilyou.public@gmail.com>"
ENV DEBIAN_FRONTEND noninteractive
ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8
ARG BUILD_DATE
RUN apt-get update && apt-get install -y \
  libdigest-perl-md5-perl \
  libgetopt-long-descriptive-perl \
  curl \
  wget \
  python-pygments \
  python-seqdiag \
  python-xdg \
  xdg-utils \
  fontconfig \
  fonts-wqy-zenhei \
  vim \
  gnupg \
  graphviz \
  dvipng \
  scrot \
  imagemagick \
  python-gtkspellcheck \
  aspell-en \
  python-gtksourceview2 \
  hicolor-icon-theme \
  libcanberra-gtk-module \
  bzr \
  git \
  locales \
  sudo \
  zim \
  --no-install-recommends \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /
RUN curl -sL http://mirror.utexas.edu/ctan/systems/texlive/tlnet/install-tl-unx.tar.gz | tar zxf - \
  && mv install-tl-20* install-tl \
  && cd install-tl \
  && echo "selected_scheme scheme-full" > profile \
  && ./install-tl -repository http://mirror.utexas.edu/ctan/systems/texlive/tlnet -profile profile \
  && cd .. \
  && rm -rf install-tl

ENV PATH /usr/local/texlive/2018/bin/x86_64-linux:$PATH

# Set the locale
RUN locale-gen zh_CN.UTF-8
ENV LANG zh_CN.UTF-8
ENV LANGUAGE zh_CN:zh
ENV LC_ALL zh_CN.UTF-8
# Replace 1000 with your user / group id 
RUN export uid=1000 gid=1000 && \ 
    mkdir -p /home/xiaox && \ 
    echo "xiaox:x:${uid}:${gid}:xiaox,,,:/home/xiaox:/bin/bash" >> /etc/passwd && \
    echo "xiaox:x:${uid}:" >> /etc/group && \
    echo "xiaox ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/xiaox && \
    chmod 0440 /etc/sudoers.d/xiaox && \
    chown ${uid}:${gid} -R /home/xiaox

USER xiaox

WORKDIR /home/xiaox
CMD [ "zim","--standalone" ]
