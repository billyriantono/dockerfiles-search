FROM chorn/arch-dev-environment:latest
LABEL maintainer="Chris Horn <chorn@chorn.com>"

ARG user="chorn"
ARG aur_packages="direnv fasd"
ENV DOTFILES_REPO="https://github.com/chorn/dotfiles"
ENV ASDF_LANGUAGES "elixir=1.5.3 nodejs=9.3.0,8.9.3 python=3.6.4 ruby=2.5.0,2.4.2 rust=beta"
ENV NODEJS_CHECK_SIGNATURES no
ENV GHQ_REPOS "chriskempson/base16-shell zdharma/fast-syntax-highlighting zsh-users/zsh-autosuggestions chorn/dev_tool_updater"
ENV BASE16 "twilight"
ENV GOPATH "/home/${user}/.go"
ENV TERM "xterm-256color"

USER ${user}:${user}
WORKDIR /home/${user}
COPY asdf_setup user_setup ./

RUN yaourt -S --noconfirm --needed --noprogressbar ${aur_packages} && \
  ./asdf_setup && rm asdf_setup && \
  ./user_setup && rm user_setup

ENTRYPOINT ["/bin/zsh", "-l"]

