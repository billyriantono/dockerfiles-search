# ArchLinux + Gitpage Blog #
# http://minibrary.com #

FROM minibrary/archlinux
MAINTAINER MiNi <minibrary@gmail.com>

# Locale to English.UTF-8 #
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

WORKDIR /root/
COPY *.sh ./

RUN chmod 755 \
  ./docker-custom.sh \
  ./git-pull.sh && \
  pacman -Syu --noconfirm && \
  ./docker-custom.sh && \
  cat ./git-pull.sh >> ~/.bashrc && \
  rm *.sh && \
  git config --global user.name minibrary && \
  git config --global user.email minibrary@gmail.com && \
  export EDITOR=nano

EXPOSE 3000

CMD ["/bin/bash"]
