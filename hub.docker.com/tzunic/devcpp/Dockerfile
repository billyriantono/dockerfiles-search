FROM ubuntu:16.04

ENV BUILD_PKGS wget curl sudo unzip bash-completion nmap cmake \ 
  clang clang-format clang-tidy python-dev python3-dev npm \
  libc++-dev build-essential qemu-system-x86 git vim-gtk exuberant-ctags \
  libncurses5-dev libclang-dev netcat pv tmux gcc-multilib libgtest-dev \
  google-mock libbz2-dev zlib1g-dev default-jre graphviz doxygen automake \
  libtool libxml2-dev pkg-config python-pip python3-pip neovim fontconfig \ 
  libreadline-dev llvm global bsdtar xclip 

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV TERM xterm-256color

ADD ycm_init.vim /root/.vimrc
ADD init.vim /root/.config/nvim/init.vim


RUN \
  locale-gen en_US.UTF-8 && \
  apt-get update && \
  apt-get install -y python-software-properties software-properties-common && \
  add-apt-repository ppa:neovim-ppa/unstable && \
  apt-get update && \
  apt-get install -y $BUILD_PKGS && \
  curl -fL https://github.com/ninja-build/ninja/releases/download/v1.7.1/ninja-linux.zip | bsdtar -xvf - && chmod +x ninja && mv ninja /usr/local/bin && \
  mkdir -p ~/.vim/autoload && \
  curl -fLo ~/.vim/autoload/plug.vim https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim && \
  curl -fLo ~/.ycm_extra_conf.py https://bitbucket.org/tzunic/devcpp/raw/master/ycm_extra_conf.py && \
  curl -fLo ~/.tmux.conf https://bitbucket.org/tzunic/devcpp/raw/master/tmux.conf && \
  pip install neovim && pip3 install neovim meson neovim-remote && \
  ln -s /usr/local/bin/meson.py /usr/local/bin/meson

RUN \
  vim +PlugInstall +qall && \
  cd ~/.vim/plugged/YouCompleteMe/ && \
  ./install.py --clang-completer --system-libclang && \
  mkdir -p /opt/vim_files && \
  mv ~/.vim  /opt/vim_files && mv ~/.vimrc /opt/vim_files && mv ~/.ycm_extra_conf.py /opt/vim_files && mv ~/.tmux.conf /opt/vim_files/ && \
  chmod -R 755 /opt/vim_files && \
  dest="/opt" && \
  curl -Lo $dest/plantuml.jar https://bitbucket.org/tzunic/devcpp/raw/master/plantuml.jar && \
  mkdir $dest/quickfix && curl -Lo $dest/quickfix/quickfix.zip https://github.com/quickfix/quickfix/archive/master.zip &&  \
  unzip $dest/quickfix/quickfix.zip -d $dest/quickfix && \
  cd $dest/quickfix/quickfix-master && ./bootstrap && ./configure --enable-static=yew --enable-shared=no && make && make install && \
  curl -L https://sourceforge.net/projects/boost/files/boost/1.60.0/boost_1_60_0.tar.gz/download | tar xzf - -C $dest && \
  cd $dest/boost_1_60_0/ && \
  ./bootstrap.sh && \
  ./b2 install --toolset=gcc  --address-model=64  && \
  ldconfig && \
  apt-get clean && rm -rf /opt/boost_1_60_0 $dest/quickfix /usr/lib/apt/lists/* /tmp/* /var/tmp/*

RUN cd /opt && curl -R -O http://www.lua.org/ftp/lua-5.3.3.tar.gz && \
  tar xf lua-5.3.3.tar.gz && cd lua-5.3.3 && make linux && make install && \
  cd .. && rm -rf lua-5.3.3 

RUN git clone --recursive https://github.com/Andersbakken/rtags && \
  cd rtags && mkdir build && cd build &&  cmake -DRTAGS_NO_ELISP_FILES=1 ../ && \
  make install && cd ../.. && rm -rf rtags 

RUN curl -fLo /root/.config/nvim/autoload/plug.vim --create-dirs \
      https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim && \
      nvim +PlugInstall +UpdateRemotePlugins +qall --headless && \
      mv /root/.config/nvim /opt/ && chmod -R 755 /opt/nvim 

