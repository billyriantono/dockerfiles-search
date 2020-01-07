# 0.11 is Ubuntu 18.04
# https://github.com/phusion/baseimage-docker
FROM phusion/baseimage:0.11

CMD ["/sbin/my_init"]


RUN apt-get update && apt-get upgrade -y -o Dpkg::Options::="--force-confold" --fix-missing

RUN apt-get install -y vim vim-nox git sudo build-essential exuberant-ctags


RUN groupadd dev
RUN useradd -m -d /home/dev -g dev -G sudo -s /bin/bash dev
RUN echo "dev:dev" | chpasswd


COPY support_files/fzf-0.17.5-linux_amd64.tgz /tmp/fzf.tgz
WORKDIR /tmp
RUN tar xf fzf.tgz
RUN cp fzf /usr/local/bin
RUN chmod +x /usr/local/bin/fzf


USER dev:dev
WORKDIR /home/dev


RUN mkdir -p /home/dev/.ssh
RUN chmod 700 /home/dev/.ssh
COPY --chown=dev:dev support_files/ssh_id_rsa /home/dev/.ssh/id_rsa
RUN chmod 600 /home/dev/.ssh/id_rsa


COPY --chown=dev:dev support_files/global_gitconfig /home/dev/.gitconfig


RUN mkdir -p /home/dev/.vim/bundle
COPY --chown=dev:dev support_files/vimrc /home/dev/.vimrc
RUN git clone https://github.com/VundleVim/Vundle.vim.git /home/dev/.vim/bundle/Vundle.vim
RUN vim +PluginInstall +qall


# You should mount your source files here, in ~/project
RUN mkdir -p /home/dev/project


USER root

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

