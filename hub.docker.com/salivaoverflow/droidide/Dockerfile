FROM ubuntu:16.04
MAINTAINER Baiqin Wang "salivaoverflow@gmail.com"
ENV LANG='en_US.UTF-8' LANGUAGE='en_US.UTF-8' LC_ALL='en_US.UTF-8'
COPY ["./.pluginlist.vim", "/root/.pluginlist.vim"]
COPY ["./.cscope_maps.vim", "/root/.cscope_maps.vim"]
COPY ["codesnippets", "/root/.vim/codesnippets"]
ARG DEBIAN_FRONTEND=noninteractive
RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment && \
	echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
	echo "LANG=en_US.UTF-8" > /etc/locale.conf && \
	apt-get update && \
	apt-get install -y --no-install-recommends apt-utils && \
	apt-get install -y locales && \
	locale-gen en_US.UTF-8 && \
	apt-get -y upgrade && \
	apt-get install -y exuberant-ctags cscope cmake clang && \
	apt-get install -y git python python-dev python3-dev wmctrl && \
	apt-get install -y ruby-full lua5.2 liblua5.2-dev libxt-dev && \
	apt-get install -y libperl-dev libx11-dev libgtk-3-dev && \
	apt-get install -y libncurses5-dev libncursesw5-dev && \
	apt-get install -y build-essential ack-grep libboost-all-dev && \
	git clone https://github.com/vim/vim.git && \
	cd vim && \
	./configure --with-features=huge --enable-pythoninterp --enable-rubyinterp --enable-luainterp \
	--enable-perlinterp --with-python-config-dir=/usr/lib/python2.7/config/ --enable-gui=gtk3 \
	--enable-cscope --prefix=/usr --enable-fail-if-missing && \
	make && make install && \
	rm -rf vim && \
	git clone https://github.com/VundleVim/Vundle.vim.git /root/.vim/bundle/Vundle.vim && \
	vim -u "/root/.pluginlist.vim" -c "PluginInstall" -c "qa!" && \
	cd /root/.vim/bundle/command-t/ruby/command-t/ext/command-t && \
	ruby extconf.rb && make && \
	mkdir /cache && cd /cache && mkdir ycm_build && mkdir llvm && \
	curl http://releases.llvm.org/6.0.1/clang+llvm-6.0.1-x86_64-linux-gnu-ubuntu-14.04.tar.xz -o llvm.tar.xz && \
	tar -xf llvm.tar.xz -C llvm/ --strip-components 1 && \
	cd ycm_build && \
	cmake -G "Unix Makefiles" -DUSE_SYSTEM_BOOST=ON -DPATH_TO_LLVM_ROOT=/cache/llvm . /root/.vim/bundle/YouCompleteMe/third_party/ycmd/cpp && \
	cmake --build . --target ycm_core && cd ~ && rm -rf /cache && \
	python /root/.vim/bundle/YouCompleteMe/install.py --clang-completer
COPY ["./.vimrc", "/root/.vimrc"]
