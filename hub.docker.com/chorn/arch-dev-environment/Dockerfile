FROM base/archlinux:latest
LABEL maintainer="Chris Horn <chorn@chorn.com>"

ARG user="chorn"
ARG timezone="/usr/share/zoneinfo/US/Eastern"
ARG locale="en_US.UTF-8"
ARG dotfiles_repo="https://github.com/chorn/dotfiles"
ARG packages="base-devel bash-completion bc cmake cscope ctags erlang-nox fzf gist git go go-tools htop imagemagick jq lua man-db man-pages mosh neovim net-tools nmap openssh openssl pass p7zip phantomjs pv python-neovim python-pip rsync shellcheck socat the_silver_searcher tmux unzip vim wget whois yarn zip zsh zsh-completions"
ARG aur_packages="ngrok"

RUN locale-gen "${locale}" && ln -sf "${timezone}" /etc/localtime && \
  pacman -Syu -qq --noconfirm --needed --noprogressbar --color never ${packages} && \
  useradd -m "${user}" && \
  echo "${user} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/docker && \
  echo -e "root:root\n${user}:${user}" | chpasswd && \
  mkdir -p /usr/src/{package-query,yaourt} && \
  chown ${user}:${user} /usr/src/{package-query,yaourt}

USER ${user}:${user}

RUN git clone https://aur.archlinux.org/package-query.git /usr/src/package-query && \
  git clone https://aur.archlinux.org/yaourt.git /usr/src/yaourt && \
  cd /usr/src/package-query && makepkg -simc --noconfirm --needed && \
  cd /usr/src/yaourt && makepkg -simc --noconfirm --needed && \
  TERM=dumb yaourt -S --noconfirm --needed --noprogressbar ${aur_packages}

