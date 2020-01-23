FROM eiel/gentoo-portage
MAINTAINER Tomohiko Himura <eiel.hal@gmail.com>

ADD make.conf /etc/portage/make.conf
RUN emerge eix portage-utils gentoolkit
RUN eix-update

RUN emerge zsh zsh-completion dev-vcs/git vim emacs tig
CMD zsh
