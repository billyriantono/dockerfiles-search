FROM ubuntu:18.04
MAINTAINER kraus1049

ENV DEFAULT_USER dev_env
ENV DEFAULT_GROUP developer
ENV DEFAULT_PASSWD passwd
ENV DEBCONF_NOWARNINGS yes
ENV DEBIAN_FRONTEND noninteractive

RUN groupadd $DEFAULT_GROUP && \
    useradd -g $DEFAULT_GROUP -m $DEFAULT_USER

RUN apt-get update && apt-get install -qy sudo \
	clang \
	clang-format \
	curl \
	fonts-ipafont \
	fonts-ipaexfont \
	git \
	gosu \
	jq \
	language-pack-ja \
	language-pack-ja-base \
	texlive-full \
	tmux \
	unzip \
	zsh \
    git gettext autoconf automake cproto \
    libxpm-dev libxmu-dev libgpm-dev \
    libacl1-dev libperl-dev \
    ruby-dev \
    build-essential curl \ 
    libncurses5-dev \
    libbonoboui2-dev \
    libcairo2-dev libxpm-dev \
    libx11-dev libxt-dev \
    libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev \
    libgtk-3-dev \ 
    lua5.2 liblua5.2-dev \
    luajit libluajit-5.1 \
    libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev llvm && ldconfig && \
    apt-get autoremove && \
    apt-get clean -yq && \
    apt-get autoclean -yq && \ 
    echo 'Defaults visiblepw' >> /etc/sudoers && \
    echo %$DEFAULT_GROUP' ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    echo $DEFAULT_USER:$DEFAULT_PASSWD | chpasswd

USER $DEFAULT_USER

ENV HOME /home/dev_env
ENV DOT_FILES "${HOME}/dotfiles"
ENV HOME_VIM "${HOME}/.vim"
ENV LOCAL_BIN "${HOME}/.local/bin"
ENV XDG_CONFIG_HOME "$HOME/.config"

WORKDIR $HOME

RUN mkdir -p $HOME/work_dir && \ 
    mkdir -p $LOCAL_BIN && \
    mkdir -p "${HOME}/.local/share"

COPY ./dotfiles ./dotfiles
COPY ./.zplug ./.zplug

RUN sudo chown -R $DEFAULT_USER:$DEFAULT_GROUP $HOME/ && \
    $HOME/dotfiles/bootstrap.sh

WORKDIR "${HOME}/.local/"

# # 一般ユーザがユーザ/グループを追加できるようにする
# # entrypoint.sh内でパーミッションを元に戻す
RUN sudo chmod u+s /usr/sbin/usermod \
    && sudo chmod u+s /usr/sbin/groupmod \
    && sudo chmod u+s /usr/sbin/useradd

COPY entrypoint.sh /opt/
RUN sudo chmod +x /opt/entrypoint.sh
ENTRYPOINT ["/opt/entrypoint.sh"]
EXPOSE 8888
CMD ["/bin/zsh"]
