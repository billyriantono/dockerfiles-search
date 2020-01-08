FROM ubuntu
COPY vimrc /vimrc
RUN buildDeps='gawk libncurses5-dev libz-dev zlib1g-dev  git ccache wget bzip2 make gcc g++ unzip python subversion file vim' \
	&& apt-get update \
	&& apt-get install -y $buildDeps \
	&& mv /vimrc /etc/vim/vimrc
