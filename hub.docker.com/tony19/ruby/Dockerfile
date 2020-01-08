FROM debian:jessie
MAINTAINER Tony Trinh <tony19@gmail.com>

ARG RUBY_VERSION=2.3.1
ARG USERNAME=app

RUN apt-get update

# install prerequisite packages here so rvm will install under non-root account
RUN apt-get install -y curl patch gawk g++ gcc make libc6-dev patch libreadline6-dev zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 autoconf libgdbm-dev libncurses5-dev automake libtool bison pkg-config libffi-dev sudo

# disable sudo password requirement to workaround no tty for _rvmsudo
RUN cp /etc/sudoers /etc/sudoers.bak
RUN echo "${USERNAME} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# install RVM for newly-created '${USERNAME}' user
RUN useradd -ms /bin/bash -g sudo "${USERNAME}" && echo "${USERNAME}:${USERNAME}" | chpasswd
USER ${USERNAME}
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN /bin/bash -l -c "\curl -sSL https://get.rvm.io | bash -s stable"
RUN /bin/bash -l -c "rvm install ${RUBY_VERSION}"
# XXX: Moved into app-specific Dockerfiles that use gemsets
# RUN /bin/bash -l -c "gem install bundler --no-ri --no-rdoc"

# restore sudo password requirement
USER root
RUN mv -f /etc/sudoers.bak /etc/sudoers

# setup user's shells for rvm
USER ${USERNAME}
RUN /bin/bash -l -c "echo 'gem: --no-ri --no-rdoc' > ~/.gemrc"
RUN /bin/bash -l -c "echo '[[ -s ~/.rvm/scripts/rvm ]] && source ~/.rvm/scripts/rvm' >> ~/.bashrc"
RUN /bin/bash -l -c "echo '[[ -s ~/.rvm/scripts/rvm ]] && source ~/.rvm/scripts/rvm' >> ~/.zshrc"

WORKDIR /home/${USERNAME}
CMD ["bash", "--login"]
