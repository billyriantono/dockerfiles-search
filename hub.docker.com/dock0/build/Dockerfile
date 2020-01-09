FROM dock0/amylum_arch
MAINTAINER akerl <me@lesaker.org>
RUN pacman -S --needed --noconfirm ruby openssh base-devel musl-amylum vim-minimal tree
RUN gem install --no-user-install --no-document targit gist
ENV EDITOR vim
WORKDIR /opt/build
CMD ["make", "local"]
