FROM dock0/arch

MAINTAINER Tomasz Tokarski tomasz@tomasztokarski.com

RUN locale-gen en_US.UTF-8
ENV LC_ALL     en_US.UTF-8
ENV LANG en_US.UTF-8
RUN locale > /etc/default/locale

RUN pacman --noconfirm -Syyu \
base-devel \
yajl \
vim \
apache-ant \
python2-sphinx \
xorg-server-xvfb \
curl \
cmake \
python2 \
python2-pip \
libevent \
zsh \
git \
xclip \
openssh \
the_silver_searcher \
desktop-file-utils \
libxrender \
libxslt \
libxtst \
eclipse \
expect \
libuv \
msgpack-c \
luajit \
lua-lpeg \
bzr \
nodejs && pacman-db-upgrade

RUN useradd -ms /bin/zsh dev
